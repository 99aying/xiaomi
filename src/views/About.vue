<template>
  <div class="about">
    <!-- <van-pull-refresh v-model="isLoading" @refresh="getJoks(2)">
      <div class="pannel" v-for="item in joks" :key="item.docid">
        <h3>{{item.title}}</h3>
        <p>{{item.summary}}</p>
      </div>
    </van-pull-refresh>
    <div style="margin:15px">
      <van-button type="primary" block @click="getJoks(1)">加载更多</van-button>
    </div> -->
    <!-- <h3 v-for="(item,index) in movies" :key="index">
      名称:{{item.MovieName}} -- 票房:{{item.amount}}万
    </h3>
    <input type="file" ref="file">
    <button @click="upImg">上传</button>
    <img :src="pic" v-if="pic" width="200" alt=""> -->
   <!-- <h1>{{add}}</h1>
    <h3 v-for="(item,index) in feiyan" :key="index">{{item.one_level_area}} {{item.sure_cnt}}</h3> -->
	
	<h4 v-for="(item) in news" :key="item.contentId">
		{{item.coverTitle}}
	</h4>
  </div>
</template>
<script>
import jsonp from '../assets/js/jsonp'
export default {
  data(){
    return {
      // joks:[],
      // page:1,
      // isLoading:false,
      movies:[],
      pic:'',
      add:'',
      // feiyan:'',
	  recommend:'',
	  news:'',
      }
  },
  created(){
    // this.getJoks();
    this.getMovies();
    this.getAdd();
    // this.getFeiyan();
	
	this.getList();
  },
  methods:{
	getList(){
		this.$http.get("http://localhost:8080/recommend/getRandContent?_t=1584940695452&csrfToken=&type=3&pageSize=10")
		.then(res=>{
			this.news = res.data.data.data
		})
	},
    // getFeiyan(){
    //   this.$http.get("http://localhost:8080/feiyan/special?uc_param_str=pccplomi&feiyan=1&district=1&tabStart=0&tabEnd=1&tabBrief=1&aid=3804775841868884355")
    //   this.$http.get("http://localhost:8080/special.json")
    //   .then(res=>{
    //     this.feiyan = res.data.data.feiyan.cities
    //     .filter(item=>item.country!="中国")
    //     .sort((a,b)=>a.sure_cnt>b.sure_cnt?-1:1);
    //   })
    //   .catch(err=>{
    //     console.log("err",err);
    //   })
    // },
    getAdd(){
      jsonp("http://api.map.baidu.com/location/ip?ak=I5p02PxH5e459CAk9vt4elbXNTkgfxde",{},
      (err,data)=>{
        this.add = data.content.address;
      })
    },
    upImg(){
      let file = this.$refs.file.files[0];
      let data = new FormData();
      data.append('file',file);
      let configs = {
        headers:{'Content-Type':'multipart/form-data'}
      }
      this.$http({
        method:'post',
        url:'/ajax/file.php',
        data,
        configs,
      })
      .then(res=>{
        console.log(res);
        if(res.data.error==0){
          this.pic = 'http://www.520mg.com'+res.data.pic;
          // 设置图片的路径
          this.$refs.file.value='';
          // 清空files文件
        }
      })
    },
    getMovies(){
      this.$http.post(
        "http://www.endata.com.cn/API/GetData.ashx", 
        "MethodName=BoxOffice_GetPcHomeList",
        {headers:{"Content-Type":"application/x-www-form-urlencoded"}}
      )
      .then(res=>{
        console.log(res.data);
        this.movies = res.data.Data.Table1.sort((a,b)=>{return a.amount>b.amount?-1:1});
      })
      .catch(err=>{
        console.log(err);
      })
      
    },
    // getJoks(type=1){
    //   if(type==2){
    //     this.isLoading = true;
    //   }
    //   // url 固定的后端给的地址
    //   this.$http.get("http://www.520mg.com/mi/list.php?page="+this.page)
    //   .then(res=>{
    //     // this.joks = res.data.result.filter(item=>item.title);
    //     // res是后端返回的数据
    //     // .data.result 返回的数据格式有个 data属性,data有result属性
    //     if(type==1){
    //       this.joks = this.joks.concat(res.data.result.filter(item=>item.title));
    //     }else if(type==2){
    //       this.joks = res.data.result.filter(item=>item.title).concat(this.joks);
    //     }
        
    //     this.page++;
    //     this.isLoading = false;
    //   })
    //   .catch(err=>{
    //     console.log(err);
    //   })
    // }
  }
}
</script>
<style>
  .pannel{
    margin: 15px;
    box-shadow: 0 3px 6px #eee;
    border-radius: 8px;
  }
  .pannel h3{
    line-height: 44px;
    padding:0 15px;
    font-size: 16px;
    font-weight: normal;
    background-color: #fafafa;
  }
  .pannel p{
    line-height: 18px;
    color: #777;
    font-size: 14px;
    padding: 15px;
  }
</style>
