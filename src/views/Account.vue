<template>
	<div>
		<div class="card-head">
			<ul class="nav-list ">
				<li>
				<router-link :to="{ path: '/index/tab1'}">
				  <span class="bg">我的主页</span>
				</router-link>
				</li>
			     <span>></span>
				<li>
					<router-link :to="{ path: '/account/info'}">
					  <span class="bg">账号设置</span>
					</router-link>
				</li>
			
				
			</ul>
		</div>
	   <div class=" card1 ">
		   <div class="nav-bar">
			   <ul class="nav-list flex-around">
				   <li >
					   <router-link to="/account/Info">
					     <span class="tit">基本信息</span>
					   </router-link>
				   </li>
					<li >
						<router-link to="/account/Email">
							 <span class="tit">邮箱</span>
						</router-link>
					</li>
					<li >
						<router-link to="/account/Password">
							 <span class="tit">密码</span>
						</router-link>
					</li>
					<li >
						<router-link to="/account/Bind">
							 <span class="tit">绑定账号</span>
						</router-link>
					</li>
			   </ul>
			   <div class="ava">
				   <hr>
			   </div>
			  
		   </div>
	    </div>
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

<style>

.ava{
	margin-top: 10px;
}
.card-head{
	margin-top: 130px;
	margin-bottom: 20px;
}


.card1 {
		width: 60%;
		height: 400px;
		background-size: 100%, 100%;
		margin-left: 150px;
		
	}

.bg{
			font-size: 18px;
			padding: 5px;
			color: rgb(86, 165, 209);
			
		}
.tit{
	font-size: 15px;
	padding: 5px;
	color: #000;
}
</style>
