<template lang="">
  <div>
   <div class="book">
       <ul>
        <li @click='detailsClick(item)' v-for="(item ,index) in bookData">
           
           <img :src="item.img" alt="">
          <p>{{item.bookname}}</p>
          <div>
            <span>￥{{item.price}}</span>
            <span>分类：{{item.booktype== '1' ? '小说' : item.booktype== '2' ? '文学' : item.booktype== '3' ? '科技':item.booktype== '4' ? '杂志' : item.booktype== '5' ? '漫画' : '外文书刊'}}</span>
          </div>
           <div class='author'>
            <span>作者:{{item.author}}</span>
            <span>数量：{{item.num}}</span>
          </div>
          <span>{{item.sellpoint}}</span>
        </li>
      
      </ul>
    </div>
  </div>
</template>
<script>


export default ({
  data() {
    return{
      booktype:5,
      bookData:""
    }
  },mounted(){
     this.$axios({
					method: "get",
					url: "http://localhost:8888/book/type",
          params:{
            booktype:2
          }
				})	.then( res =>{
						this.bookData = res.data
              console.log(this.bookData)
        })

  },methods:{
    // 跳转详情页
    detailsClick(item){
      this.$router.push({  path: "/details",query:{name:item.bookname}  });
    }
  }
 
 
})




</script>
<style scoped>
*{
  margin: 0px;
  padding: 0px;
}
li{
  list-style: none;
}
.book{
cursor: pointer;
}
.book ul{

}
.book ul li {

  display: inline-block;
  width: 21.5%;
  margin: 7px;
  padding: 10px;
  border: 1px solid #fff;
 
}
.book ul li:hover{
   border: 1px solid #999;
   box-shadow:0 0 5px #999 ;
}
.book ul li img{
  width: 100%;
}
.book ul li p{

  padding-bottom: 5px;
}
.book ul li>span{
 
  height:35px;
  overflow: hidden;
  display: inline-block;
  font-size: 13px;
  color: #999;
}
.book ul li>div span:first-child{
  color: red;
}
.book ul li>div{
  padding: 10px;
  display: flex;
  justify-content: space-between;
 
}
.author span {
  color: #999 !important;
  font-size:13px;

}
</style>
