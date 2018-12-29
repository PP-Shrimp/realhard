<style lang="less">
@import "./common.less";
</style>
<template>
  <div>
    <Row>
      <addAgent></addAgent>
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
      exportLoading: false,
      tableTitle: [
        {
          title: "代理商编号",
          key: "category1"
        },
        {
          title: "代理商名称",
          key: "category2"
        },
        {
          title: "联系人",
          key: "category3"
        },
        {
          title: "联系电话",
          key: "category4"
        },
        {
          title: "代理状态",
          key: "category5"
        },
        {
          title: "代理时间",
          key: "category6"
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
                      this.show(params.index);
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
                      this.show(params.index);
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
          category1: 156312,
          category2: "云南腾云旅行社",
          category3: "舒展",
          category4: "13596351234",
          category5: "代理中",
          category6: "2018-12-12 09:25",
          category7: "2018-12-12 09:25"
        },
        {
          category1: 156312,
          category2: "云南腾云旅行社",
          category3: "舒展",
          category4: "13596351234",
          category5: "代理中",
          category6: "2018-12-12 09:25",
          category7: "2018-12-12 09:25"
        },
        {
          category1: 156312,
          category2: "云南腾云旅行社",
          category3: "舒展",
          category4: "13596351234",
          category5: "代理中",
          category6: "2018-12-12 09:25",
          category7: "2018-12-12 09:25"
        },
        {
          category1: 156312,
          category2: "云南腾云旅行社",
          category3: "舒展",
          category4: "13596351234",
          category5: "代理中",
          category6: "2018-12-12 09:25",
          category7: "2018-12-12 09:25"
        }
      ]
    };
  },
  methods: {},
  created() {},
  mounted() {}
};
</script>
