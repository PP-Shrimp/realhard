<template>
  <div>
    <Drawer title="标准资源" v-model="value3" width="720" :mask-closable="false" :styles="styles">
      <Form ref="formData" :model="formData" :rules="checkFormData">
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="广告位名称" label-position="top" prop="name">
              <Input v-model="formData.name" placeholder="请输入广告位名称"/>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="广告位编号" label-position="top" prop="num">
              <Input v-model="formData.num" placeholder="请输入广告位编号" readonly />
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="栏目" label-position="top" prop="status">
              <Select v-model="formData.status" placeholder="请选择栏目">
                <Option value="0">首页</Option>
                <Option value="1">酒店</Option>
                <Option value="2">机票</Option>
                <Option value="3">游记</Option>
              </Select>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="广告位形式" label-position="top" prop="status">
              <Select v-model="formData.status" placeholder="请选择广告位形式">
                <Option value="0">常规广告</Option>
                <Option value="1">信息流</Option>
              </Select>
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="是否定投范围" label-position="top" prop="status">
              <Select v-model="formData.dtfw" placeholder="请选择定投范围">
                <Option value="0">支持</Option>
                <Option value="1">不支持</Option>
              </Select>
            </FormItem>
          </Col>
           <Col span="12" v-if="formData.dtfw==1">
            <FormItem label="刊例价" label-position="top" prop="status">
              <Input v-model="formData.klj" placeholder="请输入刊例价"/>
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32" v-if="formData.dtfw==0">
          <Col span="24">
            <FormItem label="广告刊例" label-position="top" prop="status"></FormItem>
            <Table :columns="tableKLTitle" :data="tableKLData" stripe></Table>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="广告位状态" label-position="top" prop="status">
              <Select v-model="formData.status" placeholder="请选择广告位状态">
                <Option value="0">运营中</Option>
                <Option value="1">暂停运营</Option>
              </Select>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="位置描述" label-position="top" prop="positionDesc">
              <Input v-model="formData.positionDesc" placeholder="请输入位置描述"/>
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="要求描述" label-position="top" prop="requireDesc">
              <Input v-model="formData.requireDesc" placeholder="请输入要求描述"/>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="是否支持连接" label-position="top" prop="status">
              <Select v-model="formData.status" placeholder="请选择代理状态">
                <Option value="0">不支持</Option>
                <Option value="1">支持内联</Option>
                <Option value="1">支持外联</Option>
              </Select>
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="上传效果图" label-position="top" prop="status">
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
              <Input type="file" placeholder="请上传效果图" :disabled="status=='view'" />
            </FormItem>
          </Col>
        </Row>
        <Row>
          <Col span="24">
            <FormItem label="素材要求" label-position="top" prop="status"></FormItem>
            <Table :columns="tableSCYQTitle" :data="tableSCYQData" stripe></Table>
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
  name: "addAdversiment",
  data() {
    const checkName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入广告位名称'));
      }
    };
    const checkPerson = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入联系人'));
      }
    };
    const checkPhone = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入联系电话'));
      }
    };
    const checkDate = (rule, value, callback) => {
      console.log(value);
      if (value[0] === '') {
        callback(new Error('请输入代理时间'));
      }
    };
    const checkPDesc = (rule, value, callback) => {//位置描述
      if (value === '') {
        callback(new Error('请输入位置描述'));
      }
    };
    const checkRDesc = (rule, value, callback) => {//要求描述
      if (value === '') {
        callback(new Error('请输入要求描述'));
      }
    };
    return {
      name:'新建',
      value3: false,
      formData:{
        name:'',
        dtfw:3,//定投范围
        klj:0,//刊例价
        positionDesc:'',//位置描述
        requireDesc:'',//要求描述
        num:'',
        person:'',
        phone:'',
        status:'',
        date:''
      },
      styles: {
        height: "calc(100% - 55px)",
        overflow: "auto",
        paddingBottom: "53px",
        position: "static"
      },
      checkFormData:{
        name:[
          { validator: checkName, trigger: 'blur' }
        ], // 名称
        person: [
          { validator: checkPerson, trigger: 'blur' }
        ],
        phone: [
          { validator: checkPhone, trigger: 'blur' }
        ],
        date: [
          { validator: checkDate, trigger: 'blur' }
        ],
        positionDesc:[
          { validator: checkPDesc, trigger: 'blur' }
        ],
        requireDesc:[
          { validator: checkRDesc, trigger: 'blur' }
        ]
      },
      tableKLTitle:[
        {
          title: "区域",
          key: "area"
        },
        {
          title: "刊例价",
          key: "klj"
        },
        {
          title: "操作",
          key: "action",
          title: "操作",
          key: "action",
          render: (h, params) => {
            return h("div", [
              h(
                "Button",
                {
                  props: {
                    type: "text",
                    size: "small"
                  },
                  on: {
                    click: () => {
                      console.log('xiugai');
                    }
                  }
                },
                "修改"
              )
            ]);
          }
        }
      ],
      tableKLData:[
        {
          area: '北京',
          klj: '156312/月',
        },
        {
          area: '北京',
          klj: '156312/月',
        }
      ],
      tableSCYQTitle:[
        {
          title:'类型',
          key:'scyqType'
        },
        {
          title:'格式',
          key:'scyqGS'
        },
        {
          title:'尺寸/字数',
          key:'scyqCCZS'
        },
        {
          title:'图片大小',
          key:'scyqSize'
        }
      ],
      tableSCYQData:[
        {
          scyqType:'图片',
          scyqGS:'jpg',
          scyqCCZS:'1234',
          scyqSize:'<=800kb'
        }
      ]
    };
  },
  props: {
    id: {
      type: String
    },
    status: {
      type: String
    }
  },
  methods: {
    DrawerToShow() {
      this.value3 = true;
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
      this.value3 = false;
      // this.$refs[name].resetFields();
    }
  },
  created() {

  },
  mounted() {

  }
};
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
