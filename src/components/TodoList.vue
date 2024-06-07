<script>
import FilterSelector from "./FilterSelector.vue";
import TodoItem from "./TodoItem.vue";

export default {
	components: {
		TodoItem, FilterSelector
	},
	data: function () {
		return {
			filter: "all",
		};
	},
	props: ["list"],
	computed: {
		completedList: function () {
			return this.list.filter((todo) => todo.completed);
		},
		activeList: function () {
			return this.list.filter((todo) => !todo.completed);
		},
		currentList: function () {
			switch (this.filter) {
				case "all":
					return this.list;
				case "active":
					return this.activeList;
				case "completed":
					return this.completedList;
			}
		},
	},
};
</script>

<template>
	<div class="todo-list-container">
		<ul>
			<todo-item v-for="todo in currentList" :item="todo" />
		</ul>
		<div v-show="list.length" class="list-footer">
			<label>Left: {{ activeList.length }}</label>
			<FilterSelector v-model="filter" />
			<button v-show="completedList.length" @click="$emit('cleared')">Clear completed</button>
		</div>
	</div>
</template>

<style scoped>
.todo-list-container {
	background-color: var(--color-panel-main);
}

ul {
	list-style: none;
	padding-inline-start: 0px;
	margin-block-start: 0px;
	margin-block-end: 0px;
}

.list-footer {
	text-align: center;
	position: relative;
	border-top: solid 1px var(--color-background);
}
.list-footer > * {
	margin: 0.8rem;
}
.list-footer > *:first-child {
	position: absolute;
	left: 0;
}
.list-footer > *:last-child {
	position: absolute;
	right: 0;
}
.list-footer > *:last-child:hover {
	text-decoration: underline;
	cursor: pointer;
}
</style>
