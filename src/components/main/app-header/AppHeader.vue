<template>
  <div class="app-header">
    <a @click="handleChange" type="text" :class="['sider-nav-toggle', collapsed ? 'collapsed' : '']"><IconFont type="outdent" :size="20" /></a>
    <div class="header-bar">
      <router-link class="logo" to="/">Admin</router-link>
      <div class="custom-content-con">
        <div class="user-dropdown">
          <Dropdown @on-click="handleClick">
            <Avatar :src="userAvator" class="user-dropdown-avator"/>
            <span>Admin</span>
            <DropdownMenu slot="list">
              <DropdownItem name="profile"><IconFont type="user"/> 个人中心</DropdownItem>
              <DropdownItem name="setting"><IconFont type="setting"/> 个人设置</DropdownItem>
              <DropdownItem name="logout" divided><IconFont type="logout"/> 退出登录</DropdownItem>
            </DropdownMenu>
          </Dropdown>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import IconFont from '_c/icon-font'
import { mapActions } from 'vuex'
export default {
  name: 'AppHeader',
  components: {
    IconFont
  },
  props: {
    collapsed: Boolean
  },
  methods: {
    ...mapActions([
      'handleLogout'
    ]),
    handleChange () {
      this.$emit('on-change', !this.collapsed)
    },
    handleClick (name) {
      switch (name) {
        case 'logout':
          this.handleLogout().then(() => {
            this.$router.push({
              name: 'login'
            })
          })
          break
      }
    }
  },
  computed: {
    userAvator () {
      return this.$store.state.user.avatorImgPath
    }
  }
}
</script>
