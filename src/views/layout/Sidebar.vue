<template>
    <el-menu mode="horizontal" theme="dark" unique-opened :default-active="$route.path" :collapse="isCollapse">
      <sidebar-item :routes='permission_routers'></sidebar-item>
    </el-menu>
</template>


<script>
import { mapGetters } from 'vuex'
import SidebarItem from './SidebarItem'
export default {
  components: { SidebarItem },
  computed: {
    ...mapGetters([
      'permission_routers',
      'sidebar'
    ]),
    isCollapse() {
      return !this.sidebar.opened
    }
  }
}
</script>
<style lang="scss">
.app-wrapper .sidebar-container[data-v-1100c946] {
  width: 100%;
  height: 180px;
  overflow-y: visible;
}
.el-menu--horizontal .el-submenu>.el-menu {
  background-color: red;
}
.el-menu--horizontal .el-submenu .el-menu-item {
  background-color: none;
}
</style>
