<template>
  <div>
    <Drawer title="新建非标广告位" v-model="value3" width="720" :mask-closable="false" :styles="styles">
      <Form ref="formData" :model="formData" :rules="checkFormData">
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="广告名称" label-position="top" prop="name">
              <Input v-model="formData.name" placeholder="请输入广告名称" :readonly="status=='view'"/>
            </FormItem>
          </Col>
          <Col span="12">
          <FormItem label="平台" label-position="top" prop="platform">
            <Select v-model="formData.platform" placeholder="请选择平台" :disabled="status=='view'">
              <Option value="0">微博</Option>
              <Option value="1">公众号</Option>
              <Option value="2">活动</Option>
              <Option value="3">直播</Option>
            </Select>
          </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
          <FormItem label="售卖方式" label-position="top" prop="sell">
            <Select v-model="formData.sell" placeholder="请选择售卖方式" :disabled="status=='view'">
              <Option value="0">CPD</Option>
            </Select>
          </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="刊例价(元／天)" label-position="top" prop="price">
              <Input type="number" v-model="formData.price" placeholder="请输入刊例价" :readonly="status=='view'"/>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="广告位状态" label-position="top" prop="status">
              <Select v-model="formData.status" placeholder="请选择广告位状态" :disabled="status=='view'">
                <Option value="0">运营中</Option>
                <Option value="1">暂停运营</Option>
              </Select>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="是否支持链接" label-position="top" prop="isLink">
              <Select v-model="formData.isLink" placeholder="请选择是否支持链接" :disabled="status=='view'">
                <Option value="0">不支持</Option>
                <Option value="1">支持内链</Option>
                <Option value="2">支持外链</Option>
              </Select>
            </FormItem>
          </Col>
          <Col span="12">
          <FormItem label="上传效果图" label-position="top" prop="picture">
            <!--<Upload
              ref="upload"
              :show-upload-list="false"
              :on-success="handleSuccess"
              :format="['jpg','jpeg','png']"
              :max-size="2048"
              :on-format-error="handleFormatError"
              :on-exceeded-size="handleMaxSize"
              :before-upload="handleBeforeUpload"
              multiple
              type="drag"
              action=""
              style="display: block;width:100%;">
              <Input type="file" v-model="formData.picture"  placeholder="请上传效果图" />
            </Upload>-->
            <Input type="file"  placeholder="请上传效果图" />
          </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
          <FormItem label="位置描述" label-position="top" prop="posDesc">
            <Input type="textarea" v-model="formData.posDesc" :rows="4" placeholder="请输入位置描述" />
          </FormItem>
          </Col>
          <Col span="12">
          <FormItem label="要求描述" label-position="top" prop="requireDesc">
            <Input type="textarea" v-model="formData.requireDesc" :rows="4" placeholder="请输入要求描述" />
          </FormItem>
          </Col>
        </Row>
      </Form>
      <div class="demo-drawer-footer">
        <Button style="margin-right: 8px" @click="cancel('formData')">取消</Button>
        <Button type="primary" @click="handleSubmit('formData')" v-if="status!='view'">保存</Button>
      </div>
    </Drawer>
  </div>
</template>
<script>
export default {
  name: 'addAdversiment',
  data () {
    const checkName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入代理商名称'))
      }
    }
    const checkPosDesc = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入位置描述'))
      }
    }
    const checkRequireDesc = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入需求描述'))
      }
    }
    return {
      name: '新建',
      value3: false,
      styles: {
        height: 'calc(100% - 55px)',
        overflow: 'auto',
        paddingBottom: '53px',
        position: 'static'
      },
      formData: {
        name: '', // 名称
        platform: '0', // 平台
        sell: '0', // 售卖方式
        price: 0, // 刊例价
        status: '0', // 广告位状态
        isLink: '2', // 是否支持链接
        picture: '', // 上传效果图
        posDesc: '', // 位置描述
        requireDesc: ''// 要求描述

      },
      checkFormData: {
        name: [
          { validator: checkName, trigger: 'blur' }
        ], // 名称
        posDesc: [
          { validator: checkPosDesc, trigger: 'blur' }
        ],
        requireDesc: [
          { validator: checkRequireDesc, trigger: 'blur' }
        ]
      },
      imgName: '',
      visible: false,
      uploadList: []
    }
  },
  props: {
    /* formData: {
      type: Object
    }, */
    status: {
      type: String
    }
  },
  methods: {
    DrawerToShow () {
      this.value3 = true
    },
    handleSubmit (name) {
      this.$refs[name].validate((valid) => {
        if (valid) {
          this.$Message.success('Success!')
        } else {
          this.$Message.error('Fail!')
        }
      })
    },
    cancel (name) {
      this.value3 = false
      // this.$refs[name].resetFields();
    },
    handleSuccess (res, file) {
      file.url = 'https://o5wwk8baw.qnssl.com/7eb99afb9d5f317c912f08b5212fd69a/avatar'
      file.name = '7eb99afb9d5f317c912f08b5212fd69a'
    },
    handleFormatError (file) {
      this.$Notice.warning({
        title: 'The file format is incorrect',
        desc: 'File format of ' + file.name + ' is incorrect, please select jpg or png.'
      })
    },
    handleMaxSize (file) {
      this.$Notice.warning({
        title: 'Exceeding file size limit',
        desc: 'File  ' + file.name + ' is too large, no more than 2M.'
      })
    },
    handleBeforeUpload () {
      const check = this.uploadList.length < 5
      if (!check) {
        this.$Notice.warning({
          title: 'Up to five pictures can be uploaded.'
        })
      }
      return check
    }
  },
  created () {

  },
  mounted () {

  }
}
</script>
<style>
.demo-drawer-footer {
  width: 100%;
  position: absolute;
  bottom: 0;
  left: 0;
  border-top: 1px solid #e8e8e8;
  padding: 10px 16px;
  text-align: right;
  background: #fff;
}
</style>
