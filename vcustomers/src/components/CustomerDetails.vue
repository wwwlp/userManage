<template>
	<div class="customerdetails container">
	<router-link to="/" class="btn btn-default">返回</router-link>
	<h1 class="page-header">
		{{customer.name}}
		<span class="pull-right">
			<router-link :to="'/edit/'+customer.id" class="btn btn-primary">编辑</router-link>
			<button class="btn btn-danger" @click="deleteCustomer(customer.id)">删除</button>
		</span>
	</h1>
	<ul class="list-group">
		<li class="list-group-item"><span class="glyphicon glyphicon-phone-alt"> {{customer.phone}}</span></li>
		<li class="list-group-item"><span class="glyphicon glyphicon-envelope"> {{customer.email}}</span></li>
	</ul>
	<ul class="list-group">
		<li class="list-group-item"><span class="glyphicon glyphicon-asterisk"> {{customer.education}}</span></li>
		<li class="list-group-item"><span class="glyphicon glyphicon-asterisk"> {{customer.graduationschool}}</span></li>
		<li class="list-group-item"><span class="glyphicon glyphicon-asterisk"> {{customer.profession}}</span></li>
		<li class="list-group-item"><span class="glyphicon glyphicon-asterisk"> {{customer.profile}}</span></li>
	</ul>
	</div>
</template>

<script>
	export default {
		name: 'customerdetails',
		data() {
			return {
				customer:""

			}
		},
		methods:{
			fetchCustomers(id){
				//			如何在点击详情时跳转至指定id用户的界面 第四步 "http://localhost:3000/users/"+id
				this.$http.get("http://localhost:3000/users/"+id)
					.then(function(response){
						this.customer = response.body
					})
			},
			deleteCustomer(id){
				this.$http.delete("http://localhost:3000/users/"+id)
					.then(function(response){
						this.$router.push({path:"/",query:{alert:"用户删除成功！"}})
					})
			}
		},
		created(){
//			如何在点击详情时跳转至指定id用户的界面 第三步 this.$route.params.id
			this.fetchCustomers(this.$route.params.id)
		}
	}
</script>

<style scoped>

</style>