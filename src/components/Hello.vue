<template>
  <div class="hello">
    <el-table :data="list" style="width: 100%">
      <el-table-column prop="number" label="编号" width="180"></el-table-column>
      <el-table-column prop="date" label="日期" width="180"></el-table-column>
      <el-table-column prop="author_name" label="作者" width="180"></el-table-column>
      <el-table-column prop="title" label="标题"></el-table-column>
    </el-table>
    <el-pagination
    layout="prev, pager, next"
    :total="total"
    :page-size="pageSize"
    @current-change="pageChange">
  </el-pagination>
  </div>
</template>

<script>


export default {
  name: 'hello',
  props: {
    url: String,
    pageSize: Number
  },
  data () {
    return {
      total: 0,
      list: [],
      json: []
    }
  },
  methods : {
    //api
    handleGetDate () {
      var result = fetch(this.url);
      result.then(res => {
          return res.json() 
        }).then(json => { 
          var json2 = JSON.parse(JSON.stringify(json));
          let json3 = json.concat(json2);
          json3.forEach((item, index) => {
            item.number = index + 1;
          })
          this.json = json3
          this.list = this.json.slice(0, this.pageSize);
          this.total = this.json.length;
        })
    },
    pageChange (val) {
      let start = (val - 1) * this.pageSize;
      this.list = this.json.slice(start, start + this.pageSize)
    }
  },
  mounted () {
    this.handleGetDate()
  }
}
</script>

