<template>
	<div class="add container">
		<h1 class="page-header">添加用户</h1>
		<form @submit="addCustomer">
			<div class="well">
				<h4>用户信息</h4>
				<div class="form-group">
					<label>姓名</label>
					<input type="text" class="form-control" placeholder="name" v-model="customer.name" />
				</div>
				<div class="form-group">
					<label>电话</label>
					<input type="text" class="form-control" placeholder="phone" v-model="customer.phone" />
				</div>
				<div class="form-group">
					<label>邮箱</label>
					<input type="text" class="form-control" placeholder="email" v-model="customer.email" />
				</div>
				<div class="form-group">
					<label>学历</label>
					<input type="text" class="form-control" placeholder="education" v-model="customer.education" />
				</div>
				<div class="form-group">
					<label>毕业学校</label>
					<input type="text" class="form-control" placeholder="graduationschool" v-model="customer.graduationschool" />
				</div>
				<div class="form-group">
					<label>职业</label>
					<input type="text" class="form-control" placeholder="profession" v-model="customer.profession" />
				</div>
				<div class="form-group">
					<label>个人简介</label>
					<textarea  class="form-control" rows="10" v-model="customer.profile" />
				</div>
				<button type="submit" class="btn btn-primary">添加</button>
			</div>
		</form>
	</div>
</template>

<script>
	export default {
		name: 'add',
		data() {
			return {
				customer:{}
			}
		},
		methods:{
			//自己绑定了submit函数，就会使用自己的函数，要阻止提交时触发的默认行为
			addCustomer(e){
				if (!this.customer.name || !this.customer.phone || !this.customer.email) {
					alert("请添加相应的信息")
				}else{
					let newCustomer = {
						name: this.customer.name,
						phone: this.customer.phone,
						email: this.customer.email,
						education: this.customer.education,
						graduationschool: this.customer.graduationschool,
						profession: this.customer.profession,
						profile: this.customer.profile
					}
					
					this.$http.post("http://localhost:3000/users", newCustomer)
						.then(function(response){
							this.$router.push({path:"/", query:{alert: "用户信息添加成功!"}});
						})
					
					e.preventDefault();
				}
				e.preventDefault();
			}
		}
	}
</script>

<style scoped>

</style>