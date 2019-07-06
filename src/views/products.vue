<template>
  <div>
    <my-header></my-header>
    <main id="main" class="container">
      <div class="pb-2 text-center">
        <img class="d-block mx-auto mb-4 w-100" src="img/index/index_guild.png">
      </div>
      <div class="row">
        <div class="col-md-9">
          <h5 class="mb-3 p-2 text-muted">笔记本电脑</h5>
          <div id="plist" class="row bg-white ml-1 mr-1 pt-2 pl-2">
            <div class="col-md-4 p-1" v-for="(p,i) of products" :key="i">
              <div class="card mb-4 box-shadow pr-2 pl-2">
                <router-link :to="`/details/${p.lid}`">
                  <img class="card-img-top" :src="p.md">
                </router-link>
                <div class="card-body p-0">
                  <h5 class="text-primary" v-text="`¥${p.price.toFixed(2)}`"></h5>
                  <p class="card-text">
                    <router-link :to="`/details/${p.lid}`" class="text-muted small" v-text="p.title"></router-link>
                  </p>
                  <div class="d-flex justify-content-between align-items-center p-2 pt-0">
                    <button class="btn btn-outline-secondary p-0 border-0" type="button">-</button>
                    <input type="text" class="form-control p-1" value="10">
                    <button class="btn btn-outline-secondary p-0 border-0" type="button">+</button>
                    <a class="btn btn-primary float-right ml-1 pl-1 pr-1" href="cart.html">加入购物车</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <h6 class="mb-3 p-2 text-muted small">
            <nav aria-label="Page navigation example">
              <ul class="pagination mb-0 justify-content-end">          
                <li class="page-item" :class="pno==='0'?'disabled':''"><a class="page-link bg-transparent" href="javascript:;">上一页</a></li>
                <li v-for="i of pageCount" :key="i" class="page-item" :class="i==parseInt(pno)+1?'active':''" @click="loadPage(i)"><a class="page-link" :class="i==parseInt(pno)+1?'border':'bg-transparent'" href="javascript:;" v-text="i"></a></li>
                <li class="page-item" :class="pno==pageCount-1?'disabled':''"><a class="page-link bg-transparent" href="javascript:;">下一页</a></li>
              </ul>
            </nav>
          </h6>
        </div>
        <div class="col-md-3 pl-0">
          <h5 class="justify-content-between align-items-center mb-1 text-muted p-2">
            <img src="img/foodstore/foodstore_icon2.png" alt=""> 商家公告
          </h5>
          <div class="bg-white small p-4 text-muted mb-3">
            <p>本店推出全网最低价套餐，保证比其他平台的价格要低！</p>
            <p>不要葱、姜、蒜等这些忌口暂时无法坐不了，敬请谅解！</p>
            <p>晚上10点以后订餐需另加送餐费2元！谢谢合作！</p>
          </div>
          <ul id="cart" class="list-group mb-3">
          <!-- <ul id="cart" class="list-group mb-3 position-fixed"> -->
            <li class="p-0 list-group-item d-flex justify-content-between lh-condensed">
              <h6 class="w-100 d-flex justify-content-between align-items-center mb-0 text-muted p-2 "> 购物车<a class="btn btn-link text-muted" href="#">清空</a>
              </h6>
            </li>
            <li class="p-0 list-group-item d-flex justify-content-between lh-condensed">
              <div class="input-group input-group-sm mt-1 mb-1">
                <div class="input-group-prepend">
                  <span class="input-group-text text-truncate bg-white p-1 border-0 d-inline-block" title="戴尔DELL灵越游匣15PR-5645B 15.6英寸游戏笔记本电脑(i5-7300HQ 8G 128GSSD+1T GTX1050 4G独显 FHD)黑">戴尔DELL灵越游匣15PR-5645B 15.6英寸游戏笔记本电脑(i5-7300HQ 8G 128GSSD+1T GTX1050 4G独显 FHD)黑</span>
                  <button class="btn btn-outline-secondary p-0 border-0" type="button">-</button>
                </div>
                <input type="text" class="form-control p-1" aria-label="Small" value="10" aria-describedby="inputGroup-sizing-sm">
                <div class="input-group-append">
                  <button class="btn btn-outline-secondary p-0 border-0" type="button">+</button>
                  <span class="input-group-text bg-white border-0 p-0 pl-1">¥59990.00</span>
                </div>
              </div>
            </li>
            <li class="p-0 list-group-item d-flex justify-content-between lh-condensed">
              <div class="input-group input-group-sm mt-1 mb-1">
                <div class="input-group-prepend">
                  <span class="input-group-text text-truncate bg-white p-1 border-0 d-inline-block" title="Apple MacBook Air 13.3英寸笔记本 银色(Core i5 处理器/8GB内存/256GB SSD闪存 MMGG2CH/A)">Apple MacBook Air 13.3英寸笔记本 银色(Core i5 处理器/8GB内存/256GB SSD闪存 MMGG2CH/A)</span>
                  <button class="btn btn-outline-secondary p-0 border-0" type="button">-</button>
                </div>
                <input type="text" class="form-control p-1" aria-label="Small" value="10" aria-describedby="inputGroup-sizing-sm">
                <div class="input-group-append">
                  <button class="btn btn-outline-secondary p-0 border-0" type="button">+</button>
                  <span class="input-group-text bg-white border-0 p-0 pl-1">¥69880.00</span>
                </div>
              </div>
            </li>
            <li class="p-0 list-group-item bg-secondary text-right">
              <img class="mb-2" src="img/foodstore/foodstore_car_2.png" alt="">
              <h4 class="d-inline-block text-white pt-2 m-0">￥129870.00</h4>
              <a class="btn btn-lg btn-primary float-right ml-1 pl-0 pr-0" href="cart.html">去结算</a>
            </li>
          </ul>
        </div>
      </div>
    </main>
  </div>
</template>
<script>
  import myHeader from '@/components/header.vue'
//node:
// module.exports={...}
  export default {
    props:["kwords"],//必须和router.js中的/:kwords保持一致
    data(){
      return {
        pno:2,
        pageCount:0,//3
        pageSize:9,
        count:0,
        products:[]
      }
    },
    created(){//当创建完组件对象时
      //this->当前组件对象
      this.load();//发送请求，首次加载页面内容
    },
    methods:{
      loadPage(i){
        this.pno=i-1;
        this.load();
      },
      load(){
        //发送ajax请求: 
        this.axios.get(
          "http://localhost:3000/products",
          {
            params:{
              kw:this.kwords,
              pno:this.pno,
            }
          }
        ).then(res=>{//必须用箭头函数
          //this->当前组件对象
          console.log(res.data);
          this.pno=res.data.pno;
          this.pageCount=res.data.pageCount;
          this.products=res.data.data;
        })
      }
    },
    watch:{//每当地址栏/macbook发生变化
      kwords(){//props中kwords变量就会自动获得变化
        //只要查询条件变化，先恢复pno为0
        this.pno=0;
        this.load();//只要kwords变化，就重新请求数据，并重新加载页面
      },
      //也可以实时监控每个模型变量的变化，来调试，并发现错误！
      pno(){
        console.log(`pno发生变化:pno=${this.pno}`);
      },
      pageCount(){
        console.log(`pageCount发生变化:pageCount=${this.pageCount}`);
      },
    },
    components:{
      myHeader
    }
  }
</script>
<style scoped>
#main{
  height:2000px;
}
/*定制小购物车部分样式*/
#main>div.row>div>h5, #main>div.row>div>h6, #cart>li:first-child>h6{
  background:linear-gradient(to bottom,#f0f0f0,#e0e0e0);
}
#cart .input-group-text{
  width:90px;
}
#cart input.form-control{
  width:25px!important;
  flex:none;
}
#cart .input-group .btn, #plist button.btn{
  width:20px;
  background:linear-gradient(to bottom,#f0f0f0,#e0e0e0);
}
#cart .input-group-append>.input-group-text{
  width:80px;
}
#cart.position-fixed{
  top:100px; right:100px
}

/*定制商品列表部分的样式*/
/*#plist button.btn{
}*/
#plist input.form-control{
  width:30px;
}
#plist+h6 .page-link{
  border-color:#bbb
}
#plist+h6 .page-link:hover{
  border-color:#007bff;
}
#plist+h6 .page-item.disabled{
  opacity:0.5;
}
</style>