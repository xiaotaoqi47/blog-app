<template>
	<div>
		
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
			</div>
		</div>
		
	</div>
</template>

<script>
export default {
	data() {
		return {
			articles: [],
			users: [],
			topics: [],
			currentIndex: 0,
			timer: null
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
	methods: {
		go() {
			this.timer = setInterval(() => {
				this.autoPlay()
			}, 3000)
		},
		stop() {
			clearInterval(this.timer)
			this.timer = null
		},
		change(index) {
			this.currentIndex = index
		},
		autoPlay() {
			this.currentIndex++
			if (this.currentIndex > this.slideList.length - 1) {
				this.currentIndex = 0
			}
		}
	}
};
</script>

<style>
</style>
