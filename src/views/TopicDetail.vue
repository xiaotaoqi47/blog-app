<template>
	<div class="container">
		<div class="row">
			<div class="col-8">
				<div class="row border-bottom">
					<div class="col-3">
						<img :src="topicVo.topic.logo" class="avatar-lg" />
						<p class="title">{{ topicVo.topic.topicName }}</p>
					</div>
					<div class="col-6">
						<p>
							<span class="sub-title">{{ topicVo.topic.articles }}篇文章,</span>
							<span class="sub-title">{{ topicVo.topic.follows }}人关注</span>
						</p>
					</div>
					<div class="col-3"><!-- <button class="btn btn-lg btn-rd warning-fill">关注</button> -->
					<!-- <li class="btn btn-lg btn-rd warning-fill" v-if="item.status" @click="changeThumbUps1(item)">关注</li>
					<li class="btn btn-lg btn-rd warning-fill" v-if="!item.status" @click="changeThumbUps1(item)" >已关注</li> -->
					</div>
				</div>
				<h3 class="title">本专题文章</h3>
				<dir class="row">
					<div v-for="(item, index) in topicVo.articleList" :key="index" class="col-12 border-bottom">
						<div class="media-wraaper">
							<div class="media-left">
								<img :src="item.author.avatar" class="avatar-lg link" />
								<p>{{ item.author.nickname }}</p>
							</div>
							<div class="media-middle">
								<router-link :to="{ path: '/article/' + item.article.id }">
									<p>{{ item.article.title }}</p>
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
				</dir>
			</div>
			<div class="col-4">
				<div class="box border-bottom">
					<p class="title">专题公告</p>
					<p class="sub-title">{{ topicVo.topic.description }}</p>
					<p>
						<a :href="topicVo.homepage">{{ topicVo.topic.homepage }}</a>
					</p>
				</div>
				<div class="box border-bottom"><p>
				分享到:<i class="iconfont" style="color: rgb(234, 111, 90);">&#xe64d;</i>
				       <i class="iconfont" style="color: rgb(135, 195, 110);">&#xe61f;</i>
				</p></div>
				<div class="box border-bottom">
					<p class="sub-title">管理员</p>
					<img :src="topicVo.admin.avatar" class="avatar-xs" />
					<p>{{ topicVo.admin.nickname }}</p>
				</div>
				<div class="box border-bottom">
					<p class="sub-title">关注的人</p>
						<div v-for="(item, index) in topicVo.articleList" :key="index" class="col-12 ">
									<img :src="item.author.avatar" class="avatar" />
									<p>{{ item.author.nickname }}</p>
						</div>
					
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			count: 9,
			currentPage: 1,
			topicVo: {}
		};
	},
	created() {
		var id = this.$route.params.id;
		this.axios.get(this.GLOBAL.baseUrl + '/topic/' + id).then(res => {
			console.log(res.data.data);
			this.topicVo = res.data.data;
		});
	},
	computed: {},
	methods: {
		changeThumbUps1(item) {
							if (item.status == 0) {
								item.status = 1
								item.fans--
							} else {
								item.status = 0
								item.fans++
							}
						}
	}
};
</script>

<style scoped>
.box {
	width: 90%;
	margin: 0 auto;
	padding: 15px;
	min-height: 100px;
}
.box > p {
	line-height: 20px;
}
@font-face {
  font-family: 'iconfont';  /* project id 1432509 */
  src: url('//at.alicdn.com/t/font_1432509_1i9vqpkaitkj.eot');
  src: url('//at.alicdn.com/t/font_1432509_1i9vqpkaitkj.eot?#iefix') format('embedded-opentype'),
  url('//at.alicdn.com/t/font_1432509_1i9vqpkaitkj.woff2') format('woff2'),
  url('//at.alicdn.com/t/font_1432509_1i9vqpkaitkj.woff') format('woff'),
  url('//at.alicdn.com/t/font_1432509_1i9vqpkaitkj.ttf') format('truetype'),
  url('//at.alicdn.com/t/font_1432509_1i9vqpkaitkj.svg#iconfont') format('svg');
}
@font-face {
  font-family: 'iconfont';  /* project id 1432509 */
  src: url('//at.alicdn.com/t/font_1432509_k99amrdnmcd.eot');
  src: url('//at.alicdn.com/t/font_1432509_k99amrdnmcd.eot?#iefix') format('embedded-opentype'),
  url('//at.alicdn.com/t/font_1432509_k99amrdnmcd.woff2') format('woff2'),
  url('//at.alicdn.com/t/font_1432509_k99amrdnmcd.woff') format('woff'),
  url('//at.alicdn.com/t/font_1432509_k99amrdnmcd.ttf') format('truetype'),
  url('//at.alicdn.com/t/font_1432509_k99amrdnmcd.svg#iconfont') format('svg');
}
.iconfont{
	font-family:"iconfont"!important;
	font-size:22px;
	font-style:normal;
	color:#aaa;
	-webkit-font-smoothing: antialiased;
	-webkit-text-stroke-width: 0.2px;
	-moz-osx-font-smoothing: grayscale;
	padding-left: 10px;
	
}
.avatar{
	height: 50px;
	width: 50px;
	border-radius: 50%;
	margin-top: 5px;
}
</style>
