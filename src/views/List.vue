<template>
	<div>
		<ul>
			<li><h3>name</h3><h3>star</h3></li>
			<template v-for="item in list">
				<li :key="item.id"><p>{{item.name}}</p> <p>{{item.stargazers_count}}</p></li>
			</template>
		</ul>
	</div>
</template>
<script type="text/javascript">
	export default{
		data(){
			return{
				list:[]
			}
		},
		methods:{
			getList(){
				let _this = this;
				this.$http.get('//api.github.com/search/repositories?q=javascript&sort=stars').then(res=>{
					console.log(res);
					if(res.data.items.length>0){
						_this.list = res.data.items
					}
				}).catch(err=>{
					console.log(err);
				})
			}
		},
		mounted(){
			this.getList();
		}

	}

// https://api.github.com/search/repositories?q=language:javascript&sort=stars

</script>
<style scoped lang="scss">
*{
	margin:0;
	padding:0;
}
ul{
	width:90%;
	margin:0 auto;
	li{
		list-style:none;
		display:flex;
		flex-direction:row;
		justify-content:space-between;
	}
}
</style>