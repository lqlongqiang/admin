<template>
  <div id="Aside">
    <div class="Navigation">
      <el-row class="tac" style="width: 200px;" v-if="flag === true">
        <el-col :span="12" style="width: 200px;">
          <el-menu
            default-active="0"
            class="el-menu-vertical-demo"
            background-color="#ffffff"
            text-color="#aaaaaa"
            active-text-color="#409EFF"
            style="width: 200px;"
            :collapse="isCollapse"
            :collapse-transition="true"
          >
            <el-menu-item
              v-for="(item, index) in NavigationBan"
              :key="item.title"
              :index="index.toString()"
              @click="NavigationJump(item, index)"
              v-show="index < 3"
              :class="{ isActives: index === activeindex }"
            >
              <template slot="title">
                <i :class="item.icon"></i>
                <span slot="title">{{ item.title }}</span>
              </template>
            </el-menu-item>
            <el-submenu
              v-for="(item, index) in NavigationBan"
              :key="index"
              v-show="index > 2"
              :index="index.toString()"
            >
              <template slot="title">
                <i :class="item.icon"></i>
                <span slot="title">{{ item.title }}</span>
              </template>
              <el-menu-item-group
                v-for="(item1, index1) in navigationban"
                :key="index1"
                v-show="index === 3"
              >
                <el-menu-item
                  @click="NavigationJumped(item1, index1)"
                  :index="index1.toString() + 4"
                  class="item_style"
                  >{{ item1.title }}</el-menu-item
                >
              </el-menu-item-group>
              <el-menu-item-group v-show="index === 4">
                <el-menu-item
                  index="4"
                  class="item_style"
                  @click="childJump(item, index)"
                >
                  分布表单
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </el-col>
      </el-row>
      <el-row class="tac" style="width: 100px;" v-else>
        <el-col :span="12" style="width: 100px;">
          <el-menu
            default-active="0"
            class="el-menu-demo"
            background-color="#ffffff"
            text-color="#aaaaaa"
            active-text-color="#409EFF"
            style="width: 100px;"
            :collapse="isCollaps"
            :collapse-transition="true"
          >
            <el-menu-item
              v-for="(item, index) in NavigationBan"
              :key="item.title"
              :index="index.toString()"
              @click="NavigationJump(item)"
            >
              <i :class="item.icon"></i>
              <span slot="title">{{ item.title }}</span>
            </el-menu-item>
          </el-menu>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  components: {},
  props: {
    flag: {
      type: Boolean
    }
  },
  data() {
    return {
      isCollapse: false, //控制折叠侧边栏
      isCollaps: true, //控制折叠侧边栏
      activeindex: 0, //
      NavigationBan: [
        {
          title: "首页",
          icon: "el-icon-house",
          path: "/Homepage"
        },
        {
          title: "日程管理",
          icon: "el-icon-date",
          path: "/Tasks"
        },
        {
          title: "通讯录",
          icon: "el-icon-document",
          path: "/mailList"
        },
        {
          title: "组织员工",
          icon: "el-icon-user",
          name: "employees"
        },
        {
          title: "表单页",
          icon: "el-icon-files",
          path: "/FormPage"
        }
      ], //侧边栏数据
      navigationban: [
        {
          title: "offer管理",
          path: "/OrganizeStaff/Offer"
        },
        {
          title: "人员信息",
          path: "/OrganizeStaff/Personnel"
        },
        {
          title: "薪酬管理",
          path: "/OrganizeStaff/Payment"
        }
      ] //侧边栏嵌套内容
    };
  },
  methods: {
    //跳转侧边栏路由
    NavigationJump(item, index) {
      //console.log(index);
      this.$router.push({ path: item.path });
      this.activeindex = index;
    },
    //子路由跳转
    NavigationJumped(item1, index1) {
      this.$router.push({ path: item1.path });
      this.activeindex = index1 + 6;
    },
    //表单页跳转
    childJump(item, index) {
      this.$router.push({ path: item.path });
      this.activeindex = index;
      //console.log(item);
    }
  },
  mounted() {},
  created() {},
  filters: {},
  computed: {},
  watch: {},
  directives: {}
};
</script>

<style scoped lang="scss">
#Aside {
  position: fixed;
  top: 40px;
  left: 0px;
}
</style>
