<template>
  <div>
    <pager :totalPage="totalPage" v-on:changed="pagerChange"></pager>
  </div>
</template>
<script>
import pager from '@/components/pager'

export default {
  name: 'index',
  data () {
    return {
      totalPage:10
    }
  },
  methods:{
    pagerChange:function(page){
      console.log(page)
    }
  },
  created (){
    
  },
  components : {
    pager
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
