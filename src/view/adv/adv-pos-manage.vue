<style lang="less">
@import "./common.less";
</style>
<template>
  <div>
    <Row>
      <Button @click="showAdd('','add')" type="primary">新建非标资源</Button>
      <Button @click="queryShow" type="primary" style="margin-left: 10px;">过滤
        <Icon type="ios-arrow-down"></Icon>
      </Button>
      <addAdversiment :id="curId" :status="status" ref="addDrawer"></addAdversiment>
      <normalAdversiment :id="curId" :status="status" ref="normalDrawer"></normalAdversiment>
    </Row>
    <Row v-if="queryFlag" style="padding:20px 20px 0;">
      <Form :model="queryData" :label-width="80">
        <Col span="8">
          <FormItem label="广告名称" label-position="top" prop="name">
            <Input v-model="queryData.name" placeholder="请输入广告名称" :readonly="status=='view'"/>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="类型" label-position="top" prop="type">
            <Select v-model="queryData.type" placeholder="请选择类型">
              <Option value="0">非标资源</Option>
              <Option value="1">标准资源</Option>
            </Select>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="平台" label-position="top" prop="terrace">
            <Select v-model="queryData.terrace" placeholder="请选择平台" :disabled="status=='view'">
              <Option value="0">微博</Option>
              <Option value="1">公众号</Option>
              <Option value="2">活动</Option>
              <Option value="3">直播</Option>
            </Select>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="栏目" label-position="top" prop="column">
            <Input v-model="queryData.column" placeholder="请输入栏目" :readonly="status=='view'"/>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="售卖方式" label-position="top" prop="saletype">
            <Select v-model="queryData.saletype" placeholder="请选择售卖方式" :disabled="status=='view'">
              <Option value="0">CPD</Option>
            </Select>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="广告位状态" label-position="top" prop="state">
            <Select v-model="queryData.state" placeholder="请选择广告位状态" :disabled="status=='view'">
              <Option value="0">运营中</Option>
              <Option value="1">暂停运营</Option>
            </Select>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="位置" label-position="top" prop="position">
            <Input v-model="queryData.position" placeholder="请输入位置" :readonly="status=='view'"/>
          </FormItem>
        </Col>
        <Col span="24">
          <FormItem>
            <Button type="primary">过滤</Button>
          </FormItem>
        </Col>
      </Form>
    </Row>
    <Row class="margin-top-10">
      <Table :columns="tableTitle" :data="tableData" stripe></Table>
      <div style="margin: 10px;overflow: hidden">
        <div style="float: right;">
          <Page :total="total" :current="pageNo" @on-change="changePage" show-total></Page>
        </div>
      </div>
    </Row>
  </div>
</template>
<script>
import addAdversiment from "@/components/adversiment/addAdversiment.vue";
import normalAdversiment from "@/components/adversiment/normalAdversiment.vue";
export default {
  name: "adv-pos-manage",
  components: {
    addAdversiment,
    normalAdversiment
  },
  data() {
    return {
      curId: "",
      status: "",
      total: 50, //总记录条数
      count: 5, //总页数
      pageNo: 1, //当前页
      queryFlag: false,
      queryData: {
        name: "",
      },
      tableTitle: [
        {
          title: "编号",
          key: "num"
        },
        {
          title: "广告位名称",
          key: "name"
        },
        {
          title: "类型",
          key: "type",
          render: (h, params) => {
            let type = "";
            params.row.type == 1 ? (type = "标准资源") : (type = "非标资源");
            return h("span", {}, type);
          }
        },
        {
          title: "平台",
          key: "terrace"
        },
        {
          title: "栏目",
          key: "column"
        },
        {
          title: "售卖方式",
          key: "saletype"
        },
        {
          title: "状态",
          key: "state",
          render: (h, params) => {
            let type = "";
            params.row.type == 1 ? (type = "运营中") : (type = "暂停运营");
            return h("span", {}, type);
          }
        },
        {
          title: "位置",
          key: "position"
        },
        {
          title: "创建时间",
          key: "createtime"
        },
        {
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
                      params.row.type == 1
                        ? this.showNormal(params.row.id, "view")
                        : this.showAdd(params.row.id, "view");
                    }
                  }
                },
                "查看"
              ),
              h(
                "Button",
                {
                  props: {
                    type: "text",
                    size: "small"
                  },
                  on: {
                    click: () => {
                      params.row.type == 1
                        ? this.showNormal(params.row.id, "edit")
                        : this.showAdd(params.row.id, "edit");
                    }
                  }
                },
                "编辑"
              ),
              h(
                "Button",
                {
                  props: {
                    type: "text",
                    size: "small"
                  },
                  on: {
                    click: () => {
                      params.row.type == 1
                        ? this.showNormal(params.row.id, "view")
                        : this.showAdd(params.row.id, "view");
                    }
                  }
                },
                "资源排期"
              )
            ]);
          }
        }
      ],
      tableData: [
        {
          id: 1,
          num: 156312,
          name: "云南腾云旅行社",
          type: 1,
          terrace: "APP",
          column: "代理中",
          saletype: "CPD",
          state: 1,
          position: "2018-12-12 09:25",
          createtime: "2018-12-12 09:25"
        },
        {
          id: 2,
          num: 156312,
          name: "云南腾云旅行社",
          type: 2,
          terrace: "APP",
          column: "代理中",
          saletype: "CPD",
          state: 2,
          position: "2018-12-12 09:25",
          createtime: "2018-12-12 09:25"
        }
      ]
    };
  },
  methods: {
    // id:当前行数据
    // view:编辑 or 查看
    // 新建非标-查看-编辑
    showAdd(id, view) {
      this.curId = id + "" || "";
      this.status = view;
      this.$refs.addDrawer.DrawerToShow();
    },
    // 标准-查看-编辑
    showNormal(id, view) {
      this.curId = id + "" || "";
      this.status = view;
      this.$refs.normalDrawer.DrawerToShow();
    },
    changePage() {},
    queryShow() {
      this.queryFlag = !this.queryFlag;
    }
  },
  created() {},
  mounted() {}
};
</script>
