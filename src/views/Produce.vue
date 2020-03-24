<template>
    <!-- <div>
        <h1>产品</h1>
        <h2>产品参数:{{$route.params.id}}</h2>
        <h2 v-if="$route.query.from">查询参数:{{$route.query.from}}</h2>
        <h3>path:{{$route.path}}</h3>
        <button @click="$router.go(-1)">返回</button>
        <button @click="$router.back()">返回back</button>
        <button @click="$router.go(1)">前进</button>
        <button @click="$router.forward()">前进forward</button>
        <button @click="$router.push('/')">首页</button><br>
        <button @click="$router.replace('/')">首页replace(不留当前页面历史记录)</button>
        <br>
        <router-link :to="{name:'Home'}">切换到首页按路由的名称</router-link> <br>
       <router-link :to="{name:'Produce',params:{'id':'mumu'}}">切换到produce</router-link><br>
       <router-link :to="{path:'/produce/xyz?from=中国'}">切换到produce-path</router-link>  
    </div> -->

    <div>
        <h1>产品</h1>
        <!-- <h2>产品参数:{{$route.params.id}}</h2>
        {{views}} -->
        <van-swipe>
            <van-swipe-item v-for="(item,index) in views.goods_info[current].gallery_v3" :key="index">
                <img :src="item.img_url" width="100%" alt="">
            </van-swipe-item>
        </van-swipe>
    </div>
</template>
<script>
export default {
    data(){
        return {
            views:{},
            current:0,
        }
    },
    created(){
        this.getView();
    },
    methods:{
        getView(){
            this.$http.get("http://www.520mg.com/mi/product.php?id="+this.$route.params.id)
            .then(res=>{
                console.log(res.data.data);
                this.views = res.data.data;
            })
        }
    }
}
</script>