<template>
	<li class="todo-item">
		<p class="todo-item__wrapper">
			<label>
				<input type="checkbox"
						class="todo-item__check"
						:checked="taskDone"
						@change="changeTaskToggle"
				>
				<span class="checkmark">
					<font-awesome-icon icon="check"/>
				</span>
			</label>
			<span :class="{'done': taskDone}">{{index + 1}}.</span>
			<span :class="{ 'done' : taskDone}" v-if="edited">{{ todoItem }}</span>
			<input class="todo-item__edit"
			v-else type="text" 
			:value="todoItem"
			@input="changeTodoItem"
			@keyup.enter="saveTodoItem">
		</p>
		<div class="buttons-wrapper">
			<button class="todo-item-btn" v-if="edited" @click="toggleEditButton">
				<font-awesome-icon icon="pen" />
			</button>
			<button class="todo-item-btn" v-else @click="saveTodoItem">
				<font-awesome-icon icon="save" />
			</button>

			<button class="todo-item-btn" @click="removeTodoItem">
				<font-awesome-icon icon="trash" />
			</button>
		</div>
	</li>
</template>

<script>
	export default {
		props: {
			todoItem: String,
			taskDone: Boolean,
			index: Number
		},
		data() {
			return {
				edited: true,
				newTodoItem: this.todoItem
			}
		},
		methods: {
			toggleEditButton() {
				this.edited = !this.edited;
			},
			changeTodoItem(event) {
				this.newTodoItem = event.target.value
			},
			saveTodoItem() {
				this.toggleEditButton();
				this.$emit('newItemValue', this.newTodoItem, this.index);
			},
			removeTodoItem() {
				this.$emit('removeItem', this.index);
			},
			changeTaskToggle(e) {
				this.newItemValue = e.target.checked;
				this.$emit('changeTaskToggle', this.newItemValue, this.index);
			}
		},
	}
</script>
<style lang="sass">
	.todo-item__wrapper
		margin: 0
		flex-grow: 1
	.todo-item
		display: flex
		justify-content: space-between
		margin: 5px 0
		padding: 10px 0
		border-bottom: 1px solid #D2D2D2
		&:hover .buttons-wrapper
			visibility: visible
			opacity: 1
	.buttons-wrapper
		transition: 0.5s ease
		visibility: hidden
		opacity: 0
	.todo-item__edit
		border: none
		border-bottom: 1px solid #D2D2D2
		width: 80%
		font-size: 18px
		&:focus
			border-color: #EAD7D7
	.todo-item-btn
		width: 35px
		height: 35px
		border: 1px solid #000
		padding: 0
		line-height: 0
		border-radius: 50%
		background-color: inherit
		outline: none
		cursor: pointer
		transition: 0.3s ease
		&:hover
			background-color: #000
			color: #fff
	.svg-inline--fa
		width: 15px
		height: 15px
	.done
		color: #ccc
	.todo-item__check
		visibility: hidden
		&:checked + .checkmark .fa-check
			visibility: visible
			opacity: 1
		&:checked + .checkmark
			border-color: #D2D2D2
	label
		position: relative
		cursor: pointer
		margin-right: 10px
	.checkmark
		display: flex
		align-items: center
		justify-content: center
		position: absolute
		right: 0
		top: 0
		width: 25px
		height: 25px
		border-radius: 50%
		border: 1px solid #000
		background-color: inherit
		color: #5DC2AF
	.fa-check
		visibility: hidden
		opacity: 0
		transition: 0.3s ease
</style>