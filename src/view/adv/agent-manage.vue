<style lang="less">
@import "./common.less";
</style>
<template>
  <div>
    <Row>
      <Button @click="show({},'add')" type="primary">新建</Button>
      <addAgent :formData="curRow" :status="status" ref="Drawer"></addAgent>
    </Row>
    <Row class="margin-top-10">
      <Table :columns="tableTitle" :data="tableData"></Table>
    </Row>
  </div>
</template>
<script>
import addAgent from "@/components/adversiment/addAgent.vue";
export default {
  name: "agent-manage",
  components: {
    addAgent
  },
  data() {
    return {
      curRow: {
        name:'',//名称
        num:'',//编号
        person:'',//联系人
        phone:'',//联系电话
        status: "0",//代理状态
        date: "",//时间
      },
      status:'',
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
                      this.show(params.row,'view');
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
                      this.show(params.row,'edit');
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
        },{
          num: 156512,
          name: "云南腾云旅行社1",
          person: "舒1展",
          phone: "13596351234",
          status: "代理中",
          date: "2018-12-13 09:25",
          category7: "2018-12-12 09:25"
        },
      ]
    };
  },
  methods: {
    // row:当前行数据
    // view:编辑 or 查看
    show(row,view) {
      this.curRow = row;
      this.status = status;
      this.$refs.Drawer.DrawerToShow();
    }
  },
  created() {},
  mounted() {}
};
</script>
