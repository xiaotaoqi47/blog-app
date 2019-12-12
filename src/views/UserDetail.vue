<template>
	<div class="container">
		<div class="banner flex flex-center"><img :src="userVo.user.banner" class="cover shadow" /></div>
		<div class="info">
			<img :src="userVo.user.avatar" class="avatar" />
			<h2>{{ userVo.user.nickname }}</h2>
			<p class="title-fans-left"> 写了{{userVo.user.articles}}篇文章  {{userVo.user.fans}}粉丝</p>
			<p class="title-detail">{{ userVo.user.introduction.slice(0, 300) }}</p>
			<button class="btn btn-follow" @click="show = !show">编辑个人资料</button>
		</div >
		<transition name="fade">
			<div id="edit-box" v-if="show">
				<input type="text" placeholder="昵称" v-model="userVo.user.nickname">
				<input type="text" placeholder="地址" v-model="userVo.user.introduction.slice(0,300)">
				<button class="btn btn-follow" @click="updateUser(userVo)">确定</button>
			</div>
		</transition>
		<div class="boxx">
			<div class="l-left">
		          <div class="tab">
					 <ul> 
				       <li>
					     <router-link to="/user/essay">
						      <p class="bg">文章</p>
					     </router-link>
					    </li>
					</ul>
		          </div>
				  <div class="tab">
					<ul>
					   <li>
					     <router-link to="/user/dynamic">
						      <p class="bg">关注</p>
					     </router-link>
					    </li>
					</ul>
					</div>
			</div>
			<div class="l-right">
				<router-view />
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			userVo: {
				user: {},
				articleList: {},
				show: false
			}
		};
	},
	created() {
		var id = this.$route.params.id;
		this.axios.get(this.GLOBAL.baseUrl + '/user/' + id).then(res => {
			console.log(res.data.data);
			this.userVo = res.data.data;
		});
	},
	methods: {
		updateUser:function(userVo){
			let data ={
					"id": userVo.user.id,
					"nickname": userVo.user.nickname,
					"password": userVo.user.password,
					"avatar": userVo.user.avatar,
					"address":userVo.user.address,
					"introduction":userVo.user.introduction,
			};
			var _this= this;
			axios.put('http://u2c7152733.zicp.vip/api/user',JSON.stringify(data))
			.then(function(response){
				console.log(response.data.msg);
				_this.show = false;
			})
		},
		deleteUser:function(id,index){
			alert(id+" " +index);
			var param ={
				id:id
			}
			var _this=this;
			axios.delete('http://u2c7152733.zicp.vip/api/user',{
				params:param
			})
			.then(function(response){
				console.log(response.data.msg);
				_this.users.splice(index,1);
			})
		},
		
		
	}
};
</script>
<style scoped="scoped">

.bg{
			font-size: 14px;
			padding: 5px;
			color: #f56c6c;

		}

.l-right{
			margin-left: 180px;
			margin-top: -115px;
		}

.boxx{
			width: 80%;
			margin-left: 80px;
			margin-top: 30px;
		}
.tab{
	margin-left: 120px;
}

.banner {
	width: 100%;
	height: 280px;
}
.cover {
	width: 85%;
	height: 90%;
	border-radius: 20px;
}
.info {
	position: relative;
	top: -60px;
	left: 0px;
	margin-bottom: -50px;
	text-align: center;
	border-radius: 20px;
}
.info img {
	width: 100px;
	height: 100px;
	border-radius: 50%;
	border: 2px solid #fff;
	
}
.row{
	margin-left: 140px;
}
ul {
	width: 100%;
}
li {
	width: 100%;
	margin-bottom: 10px;
	border-radius: 5px;
}
li a {
	display: block;
	color: rgb(51, 51, 51);
	height: 45px;
	width: 12%;
	margin-left: -25px;
	padding-top: 10px;
	padding-left: 30px;
}
li a:hover {
	background-color: rgb(240, 250, 250);
}
.router-link-active {
	background-color: rgb(250, 250, 250);
}
.btn-follow {
	background-color: rgb(232, 181, 152);
	font-weight: 400;
	font-size: 15px;
	color: #fff;
	padding: 5px 0;
	width: 120px;
	height: 30px;
	border-radius: 10px;
	display: inline-block;
	text-align: center;
	border: none;
	outline: none;
	box-shadow: 2px 2px 5px #aaa; 
	margin-top: 10px;
	margin-bottom: 5px;
}
.btn-botton {
        width: 100px;
	    color: #f56c6c;
	    background: rgb(232, 181, 152,0.3);
	    border: 3px solid rgb(232, 181, 152,0.3);
	    border-radius: 10px;
	    padding: 10px 25px;
	    text-align: center;
	    font-size: 16px;
		margin-top: -5px;
	    -webkit-transform: scale(0.7);
	  
	
}
.sub-tit{
	margin-left: 380px;
	margin-top: -20px;
}
.tit{
	padding-top: 55px;
}
.title-detail{
	font-size: 12px;
	color: rgb(170, 170, 170);
	
}
.title-fans-left{
	font-size: 16px;
	color: rgb(119, 119, 119);
	padding-top: 13px;
	padding-bottom: 10px;
	margin-left: 0px;
	word-spacing: 15px;
}
.item{
	margin-top:15px ;
}
/*动画效果*/
			.fade-enter-active, .fade-leave-avtive{
				transition: opacity 1s;
				
			}
			.fade-enter, .fade-leave-to{
				opacity: 0;
			}
</style>
