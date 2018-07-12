<template>
  <Card>
    <div class="search-con search-con-top">
      <Select class="search-col">
        
      </Select>
      <Input clearable placeholder="输入关键字搜索" class="search-input" />
      <Button class="search-btn" type="primary"><Icon type="search"/>&nbsp;&nbsp;搜索</Button>
    </div>
    <Table border :columns="columns1" :data="data1"></Table>
  </Card>
</template>

<script>
export default {
  name: 'User',
  data () {
    return {
      columns1: [
        { title: 'Name', key: 'name' },
        { title: 'Age', key: 'age' },
        { title: 'Address', key: 'address' }
      ],
      data1: []
    }
  },
  methods: {
    handleDelete (params) {
      console.log(params)
    }
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
