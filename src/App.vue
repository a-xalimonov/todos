<script>

import TodoList from './components/TodoList.vue';
import TodoInput from './components/TodoInput.vue';
import PageSelector from './components/PageSelector.vue';

let lastPage = 1;

export default {
	components: {
		TodoList, TodoInput, PageSelector
	},
	data: function () {
		return {
			pages: [
				{
					name: 'List 1',
					list: [],
				},
			],
			selected: 0,
		};
	},
	computed: {
		selectedList: {
			get: function () {
				return this.pages[this.selected] ? this.pages[this.selected].list : null;
			},
			set: function (newList) {
				this.pages[this.selected].list = newList;
			}
		}
	},
	methods: {
		addPage: function () {
			this.pages.push({
				name: 'List ' + (++lastPage),
				list: [],
			});
			this.selected = this.pages.length - 1;
		},
		selectPage: function (selectedTodo) {
			this.selected = this.pages.findIndex(todo => todo === selectedTodo);
		},
		renamePage: function (renamedTodo, newName) {
			renamedTodo.name = newName;
		},
		deletePage: function (deletedPage) {
			this.pages = this.pages.filter(page => page !== deletedPage);
			this.selected = Math.min(this.selected, this.pages.length - 1)
			if (!this.pages.length) {
				lastPage = 0;
				this.addPage();
			}
		},
		addTodo: function (todoName) {
			this.selectedList.push({
				name: todoName,
				completed: false,
			})
		},
		toggleAll: function () {
			const value = !!this.selectedList.find(todo => !todo.completed);
			this.selectedList.forEach(todo => todo.completed = value);
		},
		clearCompleted: function () {
			this.selectedList = this.selectedList.filter(todo => !todo.completed);
		},
		deleteTodo: function (deletedTodo) {
			this.selectedList = this.selectedList.filter((todo) => todo !== deletedTodo)
		},
		toggleTodo: function (toggledTodo) {
			toggledTodo.completed = !toggledTodo.completed;
		},
		renameTodo: function (renamedTodo, newName) {
			renamedTodo.name = newName;
		}
	},
	provide: function () {
		return {
			'deleteTodo': this.deleteTodo,
			'toggleTodo': this.toggleTodo,
			'renameTodo': this.renameTodo,
			'selectPage': this.selectPage,
			'renamePage': this.renamePage,
			'deletePage': this.deletePage,
		};
	},
};
</script>

<template>
	<div id="app">
		<h1>todo</h1>
		<PageSelector :pages="pages" :selected="selected" @page-added="addPage" />
		<main>
			<TodoInput @toggled-all="toggleAll" @new-todo="addTodo" />
			<TodoList v-if="selectedList" :list="selectedList" @cleared="clearCompleted" />
		</main>
	</div>
</template>

<style scoped>
#app {
	margin: 0px auto;
	max-width: 550px;
}

h1 {
	font-size: 5rem;
	text-align: center;
	width: 100%;
	line-height: 0px;
}

main {
	box-shadow: 0px 0px 20px 0px #0000003d;
}
</style>
