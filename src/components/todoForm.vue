<template>
	<form @submit.prevent="getTaskValue">
		<input type="text" 
				placeholder="What you gonna do ?" 
				v-model="todoTask" 
				class="todo-input">
	</form>
</template>

<script>
	export default {
		data() {
			return {
				todoTask: ''
			}
		},
		methods: {
			getTaskValue() {
				if(this.todoTask === '') {
					return false;
				} else {
					this.$emit('getTask',this.todoTask);
					this.todoTask = '';
				}
			}
		}
	}
</script>

<style lang="sass">
	form
		padding: 10px 0
	ul
		margin: 0
	.todo-input
		width: 100%
		padding: 5px
		outline: none
		border: none
		border-bottom: 1px solid #D2D2D2
		font-size: 18px
		&:focus
			border-color: #EAD7D7
	::-webkit-input-placeholder
		font-size: 16px
		color: #D2D2D2
</style>