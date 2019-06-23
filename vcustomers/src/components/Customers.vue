<template>
	<div class="customers container">
		<Alert v-if="alert" :message="alert"></Alert>
		<h1 class="page-header">用户管理系统</h1>
		<!--搜索 第一步-->
		<input type="text" class="form-control" placeholder="搜索" v-model="filterInput" /><br/>
		<table class="table table-striped" border="" cellspacing="" cellpadding="">
			<thead>
				<tr>
					<th>姓名</th>
					<th>电话</th>
					<th>邮箱</th>
					<th></th>
				</tr>
			</thead>
			<tbody>
				<!--搜索 第3步 customers 改为 filterBy(customers, filterInput)-->
				<tr v-for="customer in filterBy(customers, filterInput)">
					<td>{{customer.name}}</td>
					<td>{{customer.phone}}</td>
					<td>{{customer.email}}</td>
					<!--如何在点击详情时跳转至指定id用户的界面 第二步-->
					<!--to="'/customer/'+customer.id" -->
					<td><router-link class="btn btn-default" :to="'/customer/'+customer.id">详情</router-link></td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
	import Alert from "./alert"
	export default {
		name: 'customers',
		data() {
			return {
				customers:[],
				alert:"",
				filterInput:""
			}
		},
		methods:{
			fetchCustomers(){
				this.$http.get("http://localhost:3000/users")
					.then(function(response){
						this.customers = response.body;
					})
			},
//			搜索 第2步 customers 改为 filterBy(customers, filterInput)
			filterBy(customers, value){
				return customers.filter(function(customer){
					return customer.name.match(value) || customer.email.match(value) || customer.phone.match(value)
				})
			}
		},
		created(){
			if (this.$route.query.alert) {
				this.alert = this.$route.query.alert
			}
			//在一个vue实例被生成后，要执行这个函数，以获取用户信息
			this.fetchCustomers()
		},
		updated(){
			//刷新也要执行这个函数，以获取用户信息
			this.fetchCustomers()
		},
		components:{
			Alert
		}
	}
</script>

<style>
    	input,select,option,textarea{
    		outline: none !important;
    		}
</style>