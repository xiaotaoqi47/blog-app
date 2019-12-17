<template>
	<div>
		<div class="nav primary-fill shadow">
			<div class="nav-bar">
				<ul class="nav-list flex-around">
					<li class="nav-item">
						<router-link to="/index">主页</router-link>
					</li>
					<li class="nav-item">
						<router-link to="/topics">专题</router-link>
					</li>
					<li class="nav-item">
						<router-link to="/articles">文章</router-link>
					</li>
					<li class="nav-item">
						<router-link to="/users">作者</router-link>
					</li>
					<li class="nav-item"><input type="text" class="input-box" placeholder="搜索" v-model="keywords" /></li>
					<li class="nav-item"><i class="iconfont" @click="search">&#xe62e;</i></li>
					<li class="nav-item" v-if="!this.user">
						<router-link to="/sign-in">登录</router-link>
					</li>
					<li>
						<div class="dropdown">
							<a href="#" class="dropbtn"><img :src="user.avatar" @mouseenter="this.show = true" class="avatar-lg" /></a>
							<div class="dropdown-content">
								<router-link :to="{ path: '/user/' + user.id }" v-if="this.user">个人主页</router-link>
								<router-link to="/Account">账号设置</router-link>
								<router-link to="/Topup">VIP充值</router-link>
							</div>
						</div>
					</li>
                    <!-- <router-link :to="{ path: '/user/' + user.id }" v-if="this.user"><img :src="user.avatar" @mouseenter="this.show = true" class="avatar-xs abs-center-right" /></router-link> -->
					<li class="nav-item" v-if="this.user"><a class="linka" @click="logout">退出</a></li>
				</ul>
			</div>
		</div>
		<router-view class="container" />
	</div>
</template>
<script>
	export default {
		data() {
			return {
				user: JSON.parse(localStorage.getItem('user')),
				keywords: ''
			};
		},
		created() {},
		methods: {
			logout() {
				this.user = null;
				localStorage.clear();
			},
			search() {
				let currentPath = this.$route.path;
				alert(currentPath);
				if (currentPath != '/search' || currentPath != '/search/article' || currentPath != '/search/topic' || currentPath !=
					'/search/usere') {
					this.$router.push({
						path: '/search',
						query: {
							keywords: this.keywords
						}
					});
				} else {
					this.$router.push({
						path: '/empty',
						query: {
							keywords: this.keywords
						}
					});
				}
			}
		}
	};
</script>
<style scoped>
	@font-face {
		font-family: 'iconfont';
		/* project id 1432498 */
		src: url('//at.alicdn.com/t/font_1432498_f6b8j93tqzc.eot');
		src: url('//at.alicdn.com/t/font_1432498_f6b8j93tqzc.eot?#iefix') format('embedded-opentype'),
			url('//at.alicdn.com/t/font_1432498_f6b8j93tqzc.woff2') format('woff2'),
			url('//at.alicdn.com/t/font_1432498_f6b8j93tqzc.woff') format('woff'),
			url('//at.alicdn.com/t/font_1432498_f6b8j93tqzc.ttf') format('truetype'),
			url('//at.alicdn.com/t/font_1432498_f6b8j93tqzc.svg#iconfont') format('svg');
	}

	.iconfont {
		color: #000000;
		font-family: "iconfont" !important;
		font-size: 32px;
		font-style: normal;
		-webkit-font-smoothing: antialiased;
		-webkit-text-stroke-width: 0.2px;
		-moz-osx-font-smoothing: grayscale;
		margin-left: -80px;
	}


	/* 路由激活高亮样式 */
	.router-link-active {
		background-color: rgba(0, 0, 0, 0.35);
		font-weight: 700;
	}

	.container {
		margin-top: 80px;
	}

	.box {
		margin-left: -60px;
		background-color: #E0E0E0;
	}
	.linka{
		cursor: pointer;
		margin-left: -80px;
	}

	li a,
	.dropbtn {
		display: inline-block;
		/*设置成块*/
		color: white;
		text-align: center;
		text-decoration: none;
	}
	.dropdown {
		/*display:inline-block将对象呈递为内联对象，但是对象的内容作为块对象呈递。旁边的内联对象会被呈递在同一行内，允许空格。*/
		display: inline-block;
	}
	.dropdown-content {
		display: none;
		position: absolute;
		background-color: #f9f9f9;
		min-width: 140px;
		box-shadow: rgba(0, 0, 0, 0.2);
		margin-top: 6px;
		margin-left: -35px;
	}
	.dropdown-content a {
		display: block;
		color: black;
		padding: 10px 35px;
		text-decoration: none;
	}
	.dropdown-content a:hover {
		background-color: rgb(232, 181, 152,0.5);
	}
	.dropdown:hover .dropdown-content {
		display: block;
	}
</style>
