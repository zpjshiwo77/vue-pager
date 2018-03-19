# vue-pager
基于vue封装的分页器组件

#### How to start
* 下载依赖项/install dependencies
> cnpm install

* 运行服务/run server
> cnpm run dev

* 程序默认运行在8080端口: localhost:8080

#### 使用方法
 #\\\\\\<pager :totalPage="totalPage" v-on:changed="pagerChange"></pager>\\\\\\
 
（该组件源码为components文件夹下面的pager.vue文件）

* Props:
    totalPage - 总页码数

* 触发页码改变后会返回当前页码:
    changed - 页码改变时触发
