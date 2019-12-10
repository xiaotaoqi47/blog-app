<template>
	<div class="container">
		<div class="banner flex flex-center"><img :src="userVo.user.banner" class="cover shadow" /></div>
		<div class="info">
			<img :src="userVo.user.avatar" class="avatar" />
			<h2>{{ userVo.user.nickname }}</h2>
			<p class="title-fans-left"> 写了{{userVo.user.articles}}篇文章  {{userVo.user.fans}}粉丝</p>
			<p class="title-detail">{{ userVo.user.introduction.slice(0, 300) }}</p>
			<button class="btn btn-follow">修改个人信息</button>
		</div >
		<div class="row">
			<div class="col-8">
				<div class="col-12" v-for="(item, index) in userVo.articleList" :key="index">
					<div class="media-wraaper shadow">
						<div class="media-left"><img :src="item.article.thumbnail" class="thumnail-xs" /></div>
						<div class="media-middle">
							<p class="title">{{ item.article.title }}</p>
							<p class="sub-title">{{ item.article.summary }}</p>
							
							<p class="tit">
								<span class="meta gutter ">{{ item.article.comments }}评论</span>
								<span class="meta gutter">{{ item.article.likes }}喜欢</span>
								<span class="meta ">{{ item.article.createTime.date.year }}年{{ item.article.createTime.date.month }}月{{ item.article.createTime.date.day }}日</span>
							</p>
						</div>
					</div>
				</div>
			</div>
			<div class="col-4 ">
				<div class="nav-list flex-around">
				
				</div>
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
				show: false,
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
		
		
	}
};
</script>

<style scoped="scoped">
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
	height: 50px;
	width: 50%;
	margin-left: -25px;
	padding-top: 15px;
	padding-left: 20px;
}
li a:hover {
	background-color: rgb(245, 250, 250);
}
.router-link-active {
	background-color: rgb(240, 240, 240);
}
.btn-follow {
	background-color: rgb(255, 126, 126);
	font-weight: 400;
	font-size: 15px;
	color: #fff;
	padding: 5px 0;
	width: 120px;
	height: 30px;
	border-radius: 10px;
	display: inline-block;
	text-align: center;
	margin-top: 10px;
	margin-bottom: 5px;
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
</style>
