<style lang="less">
@import "./common.less";
</style>
<template>
  <div>
    <Row>
      <Button @click="show('','add')" type="primary">新建</Button>
      <Button @click="queryShow" type="primary" style="margin-left: 10px;">过滤
        <Icon type="ios-arrow-down"></Icon>
      </Button>
      <addAdveriment :formData="curRow" :status="status" ref="Drawer"></addAdveriment>
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
import addAdveriment from "@/components/adversiment/addAdversiment.vue";
export default {
  name: "adv-pos-manage",
  components: {
    addAdveriment
  },
  data() {
    return {
      curRow: {
        name: "", //名称
        num: "", //编号
        person: "", //联系人
        phone: "", //联系电话
        status: "0", //代理状态
        date: ['','']//时间
      },
      status: "",
      total: 50, //总记录条数
      count: 5, //总页数
      pageNo: 1, //当前页
      queryFlag: false,
      queryData: {
        name:'',
        status:'0',
        date:''
      },
      tableTitle: [
        {
          title: "代理商编号",
          key: "num"
        },
        {
          title: "代理商名称",
          key: "name"
        },
        {
          title: "联系人",
          key: "person"
        },
        {
          title: "联系电话",
          key: "phone"
        },
        {
          title: "代理状态",
          key: "status"
        },
        {
          title: "代理时间",
          key: "date"
        },
        {
          title: "创建时间",
          key: "category7"
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
                      this.show(params.row, "view");
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
                      this.show(params.row, "edit");
                    }
                  }
                },
                "编辑"
              )
            ]);
          }
        }
      ],
      tableData: [
        {
          num: 156312,
          name: "云南腾云旅行社",
          person: "舒展",
          phone: "13596351234",
          status: "代理中",
          date: "2018-12-12 09:25",
          category7: "2018-12-12 09:25"
        },
        {
          num: 156512,
          name: "云南腾云旅行社1",
          person: "舒1展",
          phone: "13596351234",
          status: "代理中",
          date: "2018-12-13 09:25",
          category7: "2018-12-12 09:25"
        }
      ]
    };
  },
  methods: {
    // row:当前行数据
    // view:编辑 or 查看
    show(row, view) {
      this.curRow = row || {
        name: "", //名称
        num: "", //编号
        person: "", //联系人
        phone: "", //联系电话
        status: "0", //代理状态
        date: ['',''] //时间
      };
      this.status = view;
      this.$refs.Drawer.DrawerToShow();
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
