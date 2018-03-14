<template>
  <div class="container">
      <div class="pager">
          <span v-on:click="prevPage">上一页</span>
          <b v-for="item in list" :class="{active:item.act}" v-on:click="chosePage">{{item.text}}</b>
          <span v-on:click="nextPage">下一页</span>
          <input type="text" v-model="pageVal">
          <span class="go" v-on:click="gotoPage">go</span>
      </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      nowPage:1,
      pageVal:1,
      list:[{
        text:1,
        act:true,
      }]
    }
  },
  methods: {
    chosePage:function(e){
      var that = this
      var page = e.target.innerText
      if(page != "..." && e.target.classList.value != "active"){
        that.nowPage = parseInt(page)
        that.updataPage()
        this.changePage()
      }
    },
    nextPage:function(){
      var that = this
      if(that.nowPage < that.totalPage){
        that.nowPage++;
        that.updataPage()
        this.changePage()
      }
    },
    prevPage:function(){
      var that = this
      if(that.nowPage > 1){
        that.nowPage--;
        that.updataPage()
        this.changePage()
      }
    },
    gotoPage:function(){
      var that = this
      var page = parseInt(this.pageVal)
      if(page != that.nowPage && page > 0 && page <= that.totalPage){
        that.nowPage = parseInt(page)
        that.updataPage()
        this.changePage()
      }
    },
    updataPage:function(){
      var that = this

      if(that.totalPage <= 6){
        that.list = []
        for (var i = 0; i < that.totalPage; i++) {
          var item = {}
          item.text = i+1
          if(item.text == that.nowPage) item.act = true;
          else item.act = false;
          that.list.push(item);
        }
      }
      else{
        that.list = []
        if(that.nowPage <= 3){
          for (var i = 0; i < 4; i++) {
            var item = {}
            item.text = i+1
            if(item.text == that.nowPage) item.act = true;
            else item.act = false;
            that.list.push(item);
          }
          that.list.push({text:"...",act:false})
          that.list.push({text:that.totalPage,act:false})
        }
        else if(that.nowPage >= (that.totalPage - 2)){
          that.list.push({text:1,act:false})
          that.list.push({text:"...",act:false})
          for (var i = 3; i >= 0; i--) {
            var item = {}
            item.text = that.totalPage - i
            if(item.text == that.nowPage) item.act = true;
            else item.act = false;
            that.list.push(item);
          }
        }
        else{
          that.list.push({text:1,act:false})
          that.list.push({text:"...",act:false})
          that.list.push({text:that.nowPage,act:true})
          that.list.push({text:that.nowPage+1,act:false})
          that.list.push({text:"...",act:false})
          that.list.push({text:that.totalPage,act:false})
        }
      }
    },
    changePage:function(){
      this.$emit('changed', this.nowPage)
    }
  },
  computed: {},
  props: {
    totalPage: {
      type: Number,
      default() {
        return 1
      }
    }
  },
  created() {
    this.updataPage()
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pager{
  width: auto;
  font-size: 16px;
}
.pager span{
  display: inline-block;
  padding: 5px 20px;
  border-radius: 4px;
  color: #fff;
  background: #c8c8c8;
  font-weight: bold;
  cursor: pointer;
  margin-right: 5px;
}
.pager span.go{
  padding: 5px 7px;
}
.pager b{
  display: inline-block;
  padding: 5px 0px;
  border-radius: 4px;
  width: 30px;
  text-align: center;
  color: #fff;
  background: #c8c8c8;
  cursor: pointer;
  margin-right: 5px;
}
.pager input{
  width: 30px;
  height: 30px;
  margin-right: 5px;
  box-sizing:border-box;
  position: relative;
  top: -2px;
  text-align: center;
  font-size: 16px;
}
.pager span,.pager b{
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Chrome/Safari/Opera */
  -khtml-user-select: none; /* Konqueror */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently not supported by any browser */
}
.pager b.active{
  background: rgb(177, 34, 160);
}
</style>
