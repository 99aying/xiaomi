<!-- <template>
    <div>
        分类<br>
        <button @click="$router.push('/login?redirect=/cat')">登录</button>

    </div>
</template> -->

<template>
	<div class="category" v-if="cate.length">
		<van-nav-bar title="分类" left-arrow>
		  <van-icon name="search" slot="right" />
		</van-nav-bar>
		<div class="content">
			<div class="left" ref="left">
				<div class="item" v-for="(item,index) in cate" :key="index" :class="{'active':index==current}" @click="changeCur(index)">
					{{item.category_name}}
				</div>
			</div>
			<div class="right">
				<!-- {{this.cate[current].category_name}} -->
				<div v-for="(item,index) in cate[current].category_list" :key="index">
					<div v-if="item.view_type=='category_title'">
						{{item.body.category_name}}
					</div>
					<div v-if="item.view_type=='cells_auto_fill'">
						<img :src="item.body.items[0].img_url" :style="{width:item.body.w/100+'rem',height:item.body.h/100+'rem'}" alt="">
					</div>
					<div v-if="item.view_type=='category_group'" class="group">
						<div class="col-33" v-for="product in item.body.items" :key="product.product_name+index">
							<img :src="product.img_url" width="80%" alt="">
							<p>{{product.product_name}}</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
	export default{
		data(){
			return {
				cate:[],
				current:0,
			}
		},
		created(){
			this.getCate();
		},
		methods:{
			changeCur(index){
				this.current = index;
				let left = this.$refs.left;
				let items = document .querySelectorAll(".left .item");
				let el = items[index];
				let leftH = left.offsetHeight;
				left.scrollTop = el.offsetTop-leftH/2-el.offsetHeight/2;
			},
			getCate(){
				this.$http.get("/mi/category.php")
				.then(res=>{
					// console.log(res.data);
					this.cate = res.data.data;
				})
				.catch(err=>{
					console.log(err);
				})
			}
		}
	}
</script>
<style scoped>
	.group{
		display: flex;
		flex-wrap: wrap;
	}
	.col-33{
		width: 33.333%;
		flex-basis: 33.333%;
		max-width: 33.333%;
		text-align: center;
		padding: 0.1rem;
		box-sizing: border-box;
	}
	.col-33 p{
		font-size: 0.2rem;
		color: #333;
		text-overflow: ellipsis;
		white-space: nowrap;
		overflow: hidden;
	}
	.item.active{
		color:#f30;
	}
	.category{
		display: flex;
		flex-direction: column;
	}
	.content{
		flex:1;
		display: flex;
		overflow: hidden;
	}
	.left{
		width: 1.5rem;
		height: 100%;
		overflow: auto;
		border-right:1px solid #fafafa;
		scroll-behavior: smooth;
	}
	.left::-webkit-scrollbar{
		display: none;	
	}
	.right{
		flex: 1;
		height: 100%;
		overflow:auto;
	}
	.left .item{
		height:0.88rem;
		line-height: 0.88rem;
		text-align: center;
		font-size: 0.24rem;
		border-bottom: 1px solid #FAFAFA#fafafa;
	}
</style>
