<template>
  <div>
    <Drawer title="标准资源" v-model="value3" width="720" :mask-closable="false" :styles="styles">
      <Form ref="formData" :model="formData" :rules="checkFormData">
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="代理商名称" label-position="top" prop="name">
              <Input v-model="formData.name" placeholder="请输入代理商名称" :readonly="status=='view'"/>
            </FormItem>
          </Col>
          <Col span="12" v-if="status!='add'">
            <FormItem label="代理商编号" label-position="top" prop="num">
              <Input v-model="formData.num" placeholder="请输入代理商编号" readonly />
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">  
          <Col span="12">
            <FormItem label="联系人" label-position="top" prop="person">
              <Input v-model="formData.person" placeholder="请输入联系人" :readonly="status=='view'"/>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="联系电话" label-position="top" prop="phone">
              <Input v-model="formData.phone" placeholder="请输入联系电话" :readonly="status=='view'"/>
            </FormItem>
          </Col>

          <Col span="12">
            <FormItem label="代理状态" label-position="top" prop="status">
              <Select v-model="formData.status" placeholder="请选择代理状态" :disabled="status=='view'">
                <Option value="0">代理中</Option>
                <Option value="1">已注销</Option>
              </Select>
            </FormItem>
          </Col>
          <Col span="12">
          <FormItem label="代理时间" label-position="top" prop="date" >
            <DatePicker :disabled="status=='view'"
              v-model="formData.date"
              type="daterange"
              placeholder="请选择代理时间"
              style="display: block"
              placement="bottom-end"
            ></DatePicker>
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
  name: "addAdversiment",
  data() {
    const checkName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入代理商名称'));
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
    return {
      name:'新建',
      value3: false,
      formData:{
        name:'',
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
        ]
      }
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
