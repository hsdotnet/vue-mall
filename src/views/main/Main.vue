<template>
  <Layout class="app-layout">
    <Header class="app-header">
      <AppHeader :collapsed="collapsed" @on-change="handleCollapsedChange" />
    </Header>
    <Layout>
      <Sider class="app-sider" hide-trigger collapsible :width="230" :collapsed-width="50" v-model="collapsed">
        <AppSiderNav accordion :active-name="$route.name" :collapsed="collapsed" @on-select="turnToPage" :menu-list="menuList" />
      </Sider>
      <Layout>
        <div v-if="isTab" class="app-tab-nav-wrapper">
          <AppTabNav :value="$route" @input="handleClick" :list="tagNavList" @on-close="handleCloseTag" />
        </div>
        <Content class="app-content-wrapper">
          <div v-if="!isTab" class="custom-bread-crumb">
            <Breadcrumb>
              <BreadcrumbItem v-for="item in breadCrumbList" :to="item.to" :key="`bread-crumb-${item.name}`">
                <Icon :type="item.icon || ''"></Icon>
                {{ showTitle(item) }}
              </BreadcrumbItem>
            </Breadcrumb>
          </div>
          <keep-alive :include="cacheList">
            <router-view/>
          </keep-alive>
        </Content>
      </Layout>
    </Layout>
  </Layout>
</template>
<script>
import AppHeader from '_c/main/app-header'
import AppSiderNav from '_c/main/app-sider-nav'
import AppTabNav from '_c/main/app-tab-nav'
import { mapMutations, mapActions } from 'vuex'
import { getNewTagList, getNextName } from '@/libs/util'
import { showTitle } from '@/libs/util'
export default {
  name: 'Main',
  components: {
    AppHeader,
    AppSiderNav,
    AppTabNav
  },
  data () {
    return {
      collapsed: false
    }
  },
  computed: {
    tagNavList () {
      return this.$store.state.app.tagNavList
    },
    tagRouter () {
      return this.$store.state.app.tagRouter
    },
    userAvator () {
      return this.$store.state.user.avatorImgPath
    },
    isTab () {
      return this.$store.state.user.isTab
    },
    cacheList () {
      return this.tagNavList.length ? this.tagNavList.filter(item => !(item.meta && item.meta.notCache)).map(item => item.name) : []
    },
    menuList () {
      return this.$store.getters.menuList
    },
    local () {
      return this.$store.state.app.local
    },
    breadCrumbList () {
      return this.$store.state.app.breadCrumbList
    }
  },
  methods: {
    ...mapMutations([
      'setBreadCrumb',
      'setTagNavList',
      'addTag'
    ]),
    ...mapActions([
      'handleLogin'
    ]),
    showTitle (item) {
      return showTitle(item, this)
    },
    turnToPage (name) {
      if (name.indexOf('isTurnByHref_') > -1) {
        window.open(name.split('_')[1])
        return
      }
      this.$router.push({
        name: name
      })
    },
    handleCollapsedChange (state) {
      this.collapsed = state
    },
    handleCloseTag (res, type, name) {
      const nextName = getNextName(this.tagNavList, name)
      this.setTagNavList(res)
      if (type === 'all') this.turnToPage('home')
      else if (this.$route.name === name) this.$router.push({ name: nextName })
    },
    handleClick (item) {
      this.turnToPage(item.name)
    }
  },
  watch: {
    '$route' (newRoute) {
      this.setBreadCrumb(newRoute.matched)
      this.setTagNavList(getNewTagList(this.tagNavList, newRoute))
    }
  },
  mounted () {
    /**
     * @description 初始化设置面包屑导航和标签导航
     */
    if(this.$store.state.user.isTab){
      this.setTagNavList()
      this.addTag(this.$store.state.app.homeRoute)
    }else{
      this.setBreadCrumb(this.$route.matched)
    }
  }
}
</script>
