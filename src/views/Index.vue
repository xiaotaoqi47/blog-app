<template>
	<div>
		<div class="row">
			<div class="col-3" v-for="(item, index) in topics" :key="index">
				<div class="card link shadow">
					<router-link :to="{ path: '/topic/' + item.id }"><img :src="item.logo" class="logo" /></router-link>
					<p class="title">{{ item.topicName }}</p>
					<p class="sub-title">{{ item.description.slice(0, 20) }}...</p>
					<p class="meta">
						<span class="gutter">{{ item.articles }}篇文章,</span>
						<span>{{ item.follows }}人关注</span>
					</p>
				</div>
			</div>
		</div>
        
		<div class="row">
			<div class="col-8">
				<h3>热门文章</h3>
				<div v-for="(item, index) in articles" :key="index" class="col-12">
					<div class="media-wraaper border">
						<div class="media-left">
							<router-link :to="{ path: '/user/' + item.article.userId }">
							<img :src="item.author.avatar" class="avatar-lg link" />
							</router-link>
							<p>{{ item.author.nickname }}</p>
							<strong>来自</strong>
							<p>{{ item.topic.topicName }}</p>
						</div>
						<div class="media-middle flex flex-around flex-left">
							<router-link :to="{ path: '/article/' + item.article.id }" class="subtitle">
								 {{ item.article.title }} 
							</router-link>
							<p class="sub-title link">{{ item.article.summary }}</p>
							<p>
								<span class="meta gutter">{{ item.article.comments }}评论</span>
								<span class="meta">{{ item.article.likes }}喜欢</span>
							</p>
						</div>
						<div class="media-right"><img :src="item.article.thumbnail" alt="" /></div>
					</div>
				</div>
			</div>
			<div class="col-4">
				<h3>热门作者</h3>
				<div v-for="(item, index) in users" :key="index" class="row">
					<div class="col-12 border box">
						<div class="flex-center-y">
							<router-link :to="{ path: '/user/' + item.id }">
							<img :src="item.avatar" class="avatar-xs link" />
							</router-link>
							<p class="sub-title">{{ item.nickname }}</p>
						</div>
						<div class="flex-center-y">
							<p class="meta">{{ item.fans }}个粉丝</p>
							<p class="meta">写了{{ item.articles }}篇文章</p>
						</div>
						<div class="flex-center-y"><button class="btn btn-follow">关注</button></div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		isActive: true
		return {
			articles: [],
			users: [],
			topics: []
		};
	},
	created() {
		this.axios.get(this.GLOBAL.baseUrl + '/article').then(res => {
			// console.log(res.data.data);
			this.articles = res.data.data;
		});
		this.axios.get(this.GLOBAL.baseUrl + '/user').then(res => {
			// console.log(res.data.data);
			this.users = res.data.data;
		});
		this.axios.get(this.GLOBAL.baseUrl + '/topic').then(res => {
			// console.log(res.data.data);
			this.topics = res.data.data;
		});
	},
	methods:{
		changeTab: function() {
			this.isActive = !this.isActive
			this.selected = this.selected == 0 ? 1 : 0
		},
	}
};
</script>

<style scoped="scoped">
.logo {
	border-top-left-radius: 5px;
	border-top-right-radius: 5px;
}
.logo:hover {
	opacity: 0.6;
}
.box {
	display: flex;
	justify-content: space-around;
	height: 70px;
	padding: 10px;
}
.btn-follow {
	background-color: #42c02e;
	font-weight: 400;
	font-size: 15px;
	color: #fff;
	padding: 5px 0;
	width: 80px;
	height: 30px;
	border-radius: 40px;
	display: inline-block;
	text-align: center;
}
.login-box{
				width: 400px;
				height:380px;
				position: fixed;
				bottom:130px;
				left:480px;  
				display: flex;
				flex-direction: column;
			}
.tab {
				display: flex;
				align-items: center;
				justify-content: space-around;
				flex: 0 0 13%;
				background-color:#fff;
				border-top-left-radius: 5px;
				border-top-right-radius: 5px;
			}
			
			.tab-item {
				cursor: pointer;
				display: inline-block;
				width: 40%;
				line-height: 40px;
				text-align: center;
				font-size: 15px;
			}
.tab-box{
				flex:1 1 87%;
				background-color:#fff;
				color: #333;
				border-bottom-left-radius: 5px;
				border-bottom-right-radius: 5px;
				display: flex;
				flex-direction: column;
				align-items: center;
				padding-top: -20px;
				padding-bottom: 10px;
			 
			}
.active {
				color: #00BBDD;
				font-weight: 600;
				border-bottom: 2px solid #00BBDD;
			}
.input-box{
				width: 80%;
				height: 60px;
				margin-bottom: 35px;
			}
			.input-box label{
				display: block;
				padding-top: 15px;
				height: 20px;
				color: red;
			}
			.input-box i{
				position: relative;
				top:33px;
			}
			.input-box input{
				display: block;
				width: 100%;
				height: 40px;
				border: 1px solid #ccc;
				color: #333;
				padding-left: 25px;
				padding-top: 5px;
			}
</style>
