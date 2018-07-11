<template>
  <div class="app-header">
    <router-link class="logo" to="/">Admin</router-link>
    <div class="header-bar">
      <a @click="handleChange" type="text" :class="['sider-trigger-a', collapsed ? 'collapsed' : '']"><Icon type="navicon-round" :size="20" /></a>
      <div class="custom-content-con">
        <div class="user-avator-dropdown">
          <Dropdown @on-click="handleClick">
            <Avatar :src="userAvator" class="user-avator"/>
            <span>Admin</span>
            <DropdownMenu slot="list">
              <DropdownItem name="logout">退出登录</DropdownItem>
            </DropdownMenu>
          </Dropdown>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'AppHeader',
  props: {
    collapsed: Boolean
  },
  methods: {
    ...mapActions([
      'handleLogOut'
    ]),
    handleChange () {
      this.$emit('on-change', !this.collapsed)
    },
    handleClick (name) {
      switch (name) {
        case 'logout':
          this.handleLogOut().then(() => {
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

<style lang="less">
  @import './app-header.less';
</style>
