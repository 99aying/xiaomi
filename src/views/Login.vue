<template>
    <div>
    <van-nav-bar
        title="登录"
        left-arrow
        @click-left="$router.go(-1)"
        />
    <van-cell-group>
        <van-field v-model="uname" placeholder="请输入用户名" />
        <van-field type="password" v-model="upwd" placeholder="请输入密码"/>
    </van-cell-group>
    <!-- <van-button round type="info" @click="login">登录</van-button> -->
    <div style="margin:15px">
        <van-button color="linear-gradient(to right bottom, #7F7FD5, #86A8E7,#91EAE4)" @click="login" round block>登录</van-button>
    </div>
        <!-- 用户名: <input type="text" v-model="uname"><br>
        <button >登录</button> -->
    </div>
</template>
<script>
import Cookie from '../assets/js/Cookie';
export default {
    data(){
        return {
            uname:"",
            upwd:"",
            }
    },
    methods:{
        login(){
            this.$http({
                method:"POST",
                url:"http://www.520mg.com/member/index_login.php",
                data:`fmdo=login&dopost=login&userid=${this.uname}&pwd=${this.upwd}`,
                configs:{withCredentials:true}
                // 允许跨域携带cookie
            })
            .then(res=>{
                console.log(res.data);
                if(res.data.status==1){
                    this.$notify({type:'success',message:res.data.msg});
                   Cookie.setCookie("uname",this.uname);
                    let redirect = this.$route.query.redirect;
                    console.log("redirect",redirect);
                    if(redirect){
                        this.$router.replace(redirect);
                    }else{
                        this.$router.replace("/user");
                    } 
                }else{
                    this.$notify({type:'danger',
                    message:res.data.msg});
                    // alert(res.data.msg)
                }
            })
            
        }
    }
}
</script>
<style scoped>
.van-nav-bar .van-icon{
    color:#777;
}
</style>