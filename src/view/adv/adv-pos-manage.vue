<style lang="less">
@import "./common.less";
</style>
<template>
  <div>
    <Row>
      <Button @click="show('','add')" type="primary">新建非标资源</Button>
      <Button @click="queryShow" type="primary" style="margin-left: 10px;">过滤
        <Icon type="ios-arrow-down"></Icon>
      </Button>
      <addAdversiment :id="curId" :status="status" ref="addDrawer"></addAdversiment>
      <normalAdversiment :id="curId" :status="status" ref="normalDrawer"></normalAdversiment>
    </Row>
    <Row v-if="queryFlag" style="padding:20px 20px 0;">
      <Form :model="queryData" :label-width="80">
        <Col span="8">
          <FormItem label="代理商名称" label-position="top" prop="name">
            <Input v-model="queryData.name" placeholder="请输入代理商名称"/>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="代理状态" label-position="top" prop="status">
            <Select v-model="queryData.status" placeholder="请选择代理状态">
              <Option value="0">代理中</Option>
              <Option value="1">已注销</Option>
            </Select>
          </FormItem>
        </Col>
        <Col span="8">
          <FormItem label="代理时间" label-position="top" prop="date">
            <DatePicker
              v-model="queryData.date"
              type="daterange"
              placeholder="请选择代理时间"
              style="display: block"
              placement="bottom-end"
            ></DatePicker>
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
        status: "0",
        date: ""
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
