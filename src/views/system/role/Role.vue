<template>
  <Card>
    <div class="search-con search-con-top">
      <Select class="search-col"></Select>
      <Input clearable placeholder="输入关键字搜索" class="search-input" />
      <Button class="search-btn" type="primary"><Icon type="search"/>&nbsp;&nbsp;搜索</Button>
    </div>
    <Table border :columns="columns" :data="data"></Table>
    <div style="height:500px;"></div>
  </Card>
</template>

<script>
import { getRoles } from '@/api/role'
export default {
  name: 'Role',
  data () {
    return {
      columns: [
        { title: '编号', key: 'roleId' },
        { title: '名称', key: 'roleName' },
        { title: '备注', key: 'remark' }
      ],
      data: []
    }
  },
  methods: {
    
  },
  mounted () {
    getRoles().then(res=> {
      console.log(res)
    })
  }
}
</script>

<style lang="less">
.search-con{
  padding: 5px 0;
  .search{
    &-col{
      display: inline-block;
      width: 200px;
    }
    &-input{
      display: inline-block;
      width: 200px;
      margin-left: 2px;
    }
    &-btn{
      margin-left: 2px;
    }
  }
}
</style>
