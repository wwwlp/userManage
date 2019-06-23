<template>
	<div :class="{active:isActive}">
		<div class="alert alert-warning alert-dismissible" role="alert">
			<button @click="close" type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button> {{message}}
		</div>
	</div>
</template>

<script>
	export default {
		name: 'alert',
		props: ["message"],
		data() {
			return {
				isActive: false
			}
		},
		methods: {
			close() {
				this.isActive = true;
			}
		}

	}
</script>

<style scoped>
	.active {
		display: none;
	}
</style>