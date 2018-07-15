<template>
  <div :class="['sider-control', open ? 'open' : '']">
    <div class="panel">
      <div class="panel-header">控制面板</div>
      <div class="panel-body">
        <Tabs class="app-tabs">
          <TabPane label="顶部导航">
            <SingleCheckboxList :list="topNavList" value="tzl" />
          </TabPane>
          <TabPane label="侧边导航">
            <SingleCheckboxList :list="siderNavList" value="ayh" />
          </TabPane>
          <TabPane label="其它">
            <SingleCheckboxList :list="otherList" />
          </TabPane>
        </Tabs>
      </div>
    </div>
  </div>
</template>

<script>
import SingleCheckboxList from '_c/single-checkbox-list'
export default {
  name: 'AppSiderControl',
  components: {
    SingleCheckboxList
  },
  data () {
    return {
      topNavList: [
        { name: 'tzl', title: '天之蓝' },
        { name: 'hzl', title: '海之蓝' },
        { name: 'mzl', title: '梦之蓝' },
        { name: 'xyh', title: '星耀黄' },
        { name: 'fyh', title: '枫叶红' },
        { name: 'gly', title: '橄榄绿' },
        { name: 'mlz', title: '魅力紫' },
        { name: 'ysy', title: '雅士银' },
        { name: 'ahy', title: '暗夜黑' }
      ],
      siderNavList: [
        { name: 'ayh', title: '暗夜黑' },
        { name: 'gdh', title: '古典灰' },
        { name: 'ysy', title: '雅士银' }
      ],
      otherList: [
        { name: 'mklj', title: '固定当前模块路径导航' },
        { name: 'yc', title: '隐藏当前模块路径导航' }
      ]
    }
  },
  computed: {
    open () {
      return this.$store.state.app.controlOpen
    }
  }
}
</script>

<style lang="less">
.sider-control{
  top:50px;
  bottom: 0;
  background:#fff;
  position:fixed;
  z-index: 100; 
  color: #333;
  transition-duration:.3s;
  transition-property:left,right;
  width:300px;
  right:-300px;
  border-left:1px solid #ddd;
  .panel{
    position:relative;
    .panel-header{
      padding: 9px 10px 10px 10px;
      font-size: 14px;
      border-bottom: 1px solid #ddd; 
    }
    .panel-body{
      padding: 5px 5px 15px 5px;
      .ivu-tabs-nav .ivu-tabs-tab{
        padding: 10px;
        margin-right: 5px !important;
      }
      .ivu-tabs .ivu-tabs-tabpane{
        padding:0 10px;
      }
    }
  }
 }
 .sider-control.open{
   right: 0;
 }
</style>
