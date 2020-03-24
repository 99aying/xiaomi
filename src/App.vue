<template>
  <div id="app">
    <transition enter-active-class="slideInRight animated" 
    leave-active-class="slideOutRight animated" 
    mode="in-out">
      <router-view class="page"/>
    </transition>
    <div id="nav">
      <router-link to="/" class="list ihome">
      首页
      </router-link> 
      <router-link to="/cat" class="list icat">
      分类</router-link>
      <router-link to="/cart" class="list icart">
      购物车</router-link>
      <router-link to="/user" class="list iuser">
      我的</router-link>
      <!-- router-link 切换页面导航 -->
    </div>
    <!-- <router-view class="page"/> -->
    <!-- router-view 存放页面 -->
  </div>
</template>

<style>
*{
  margin: 0;
  padding: 0;
}
a{
  text-decoration: none;
  color: #777;
}
.page{
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0.98rem;
  overflow: auto;
  background-color: #fff;
}
#nav{
  display: flex;
  width: 100%;
  height: 0.98rem;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  box-shadow: 0 -2px 4px rgba(200,200,200,0.4);
}
#nav a{
  flex: 1;
  /* line-height: 98px; */
  text-align: center;
}
.router-link-exact-active{
  color: #f30;
}
#nav .list{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
/* #nav .list img{
  width: 0.44rem;
  height: 0.44rem;
} */
#nav .list:before{
	content: "";
	display: block;
	width: 0.44rem;
	height: 0.44rem;
	background-image: url("./assets/home.png");
	background-size: cover;
}
#nav .router-link-active.router-link-exact-active:before{
	background-image: url("./assets/home-h.png");
}
#nav .icat:before{
	background-image: url("./assets/cat.png");
}
#nav .router-link-active.icat:before{
	background-image: url("./assets/cat-h.png");
}
#nav .icart:before{
	background-image: url("./assets/cart.png");
}
#nav .router-link-active.icart:before{
	background-image: url("./assets/cart-h.png");
}
#nav .iuser::before{
	background-image: url("./assets/user.png");
}
#nav .router-link-active.iuser:before{
	background-image: url("./assets/user-h.png");
}
</style>
