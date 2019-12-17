<template>
	<div>
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
					<p class="sub-tit"><button class="btn btn-botton" @click="deleteUser(item.id,index)">删除</button></p>
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
			userVo: {
				user: {},
				articleList: {},
			
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
</style>
