<template>
	<div class="login_layout">
		<h2>欢迎登录</h2>
		<form v-if="!isReg">
			<input type="text" v-model="name" placeholder="用户名" />
			<a>忘记登录用户名</a>
			<input type="password" v-model="password" placeholder="密码" />
			<a>忘记密码</a>
			<div class="btn1">
				<button class="button--border--right button--base" @click="login()" type="button">登录</button>
				<button class="button--base" @click="reg()" type="button">注册</button>
			</div>
		</form>
		<form v-else>
			<label>用户名：</label>
			<input type="text" value="" v-model="name" /><br /><br />
			<label>密码：</label>
			<input type="password" value="" v-model="password" /><br /><br />
			<label>请再次输入密码：</label>
			<input type="password" value="" v-model="repeat" /><br /><br />
			<div class="btn1">
			<button class="button--border--right button--base" @click="addUser()" type="button">确定</button>
			<button class="button--base" @click="cancel()" type="button">取消</button>
			</div>
		</form>
	</div>

</template>

<script>
	export default {
		name: "login",
		data() {
			return {
				isReg: false,
				name: "",
				password: "",
				repeat: ""
			}
		},
		methods: {
			login() {
				if(localStorage.getItem("name") === this.name && localStorage.getItem("password") === this.password) {
					this.name = "";
					this.password = "";
					this.$router.push("/")
				} else {
					alert("输入错误")
				}
			},
			reg() {
				this.isReg = true;
			},
			addUser() {
				if(this.password === this.repeat) {
					localStorage.setItem("name", this.name);
					localStorage.setItem("password", this.password);
					this.name = "";
					this.password = "";
					this.isReg = false;
				} else {
					alert("密码输入不一致");
					this.password = "";
					this.repeat = "";
				}
			},
			cancel() {
				this.isReg = false;
			}
		}
	}
</script>

<style>
	*{
	margin: 0;
	padding: 0;
	list-style: none;
}
a{
	text-decoration: none;
}

	
	.btn1 {
		width: 100%;
		display: flex;
	}
	
	.button--base {
		flex: 1;
		box-sizing: border-box;
		font-size: 15px;
		height: 30px;
		background: #42B983;
		color: white;
		outline: none;
		border: none;
		margin: 20px 0px;
	}
	.button--border--right{
		border-right: white 1px solid !important;
	}
	
	input,textarea{
		outline: none;
		border: #42B983 1px solid;
		width: 100%;
		height: 30px;
		box-sizing: border-box;
		padding: 0 10px;
		font-size: 15px;
	}
	.login_layout {
		max-width: 300px;
		margin: 0 auto;
		position: relative;
	}
	
	.login_layout h2 {
		margin: 50px 0;
		text-align: center;
	}
	
	.login_layout a {
		font-size: 13px;
		color: cornflowerblue;
		float: right;
		margin-bottom: 25px;
		margin-top: 5px;
	}
	
</style>