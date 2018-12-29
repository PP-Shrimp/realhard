<template>
  <div>
    <Button @click="value3 = true" type="primary">新建</Button>
    <Drawer title="Create" v-model="value3" width="720" :mask-closable="false" :styles="styles">
      <Form :model="formData">
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="Name" label-position="top">
              <Input v-model="formData.name" placeholder="please enter user name"/>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="Url" label-position="top">
              <Input v-model="formData.url" placeholder="please enter url">
                <span slot="prepend">http://</span>
                <span slot="append">.com</span>
              </Input>
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="Owner" label-position="top">
              <Select v-model="formData.owner" placeholder="please select an owner">
                <Option value="jobs">Steven Paul Jobs</Option>
                <Option value="ive">Sir Jonathan Paul Ive</Option>
              </Select>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="Type" label-position="top">
              <Select v-model="formData.type" placeholder="please choose the type">
                <Option value="private">Private</Option>
                <Option value="public">Public</Option>
              </Select>
            </FormItem>
          </Col>
        </Row>
        <Row :gutter="32">
          <Col span="12">
            <FormItem label="Approver" label-position="top">
              <Select v-model="formData.approver" placeholder="please choose the approver">
                <Option value="jobs">Steven Paul Jobs</Option>
                <Option value="ive">Sir Jonathan Paul Ive</Option>
              </Select>
            </FormItem>
          </Col>
          <Col span="12">
            <FormItem label="DateTime" label-position="top">
              <DatePicker
                v-model="formData.date"
                type="daterange"
                placeholder="please select the date"
                style="display: block"
                placement="bottom-end"
              ></DatePicker>
            </FormItem>
          </Col>
        </Row>
        <FormItem label="Description" label-position="top">
          <Input
            type="textarea"
            v-model="formData.desc"
            :rows="4"
            placeholder="please enter the description"
          />
        </FormItem>
      </Form>
      <div class="demo-drawer-footer">
        <Button style="margin-right: 8px" @click="value3 = false">Cancel</Button>
        <Button type="primary" @click="value3 = false">SUB</Button>
      </div>
    </Drawer>
  </div>
</template>
<script>
export default {
  name: "addAdversiment",
  data() {
    return {
      value3: false,
      styles: {
        height: "calc(100% - 55px)",
        overflow: "auto",
        paddingBottom: "53px",
        position: "static"
      },
      formData: {
        name: "",
        url: "",
        owner: "",
        type: "",
        approver: "",
        date: "",
        desc: ""
      }
    };
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