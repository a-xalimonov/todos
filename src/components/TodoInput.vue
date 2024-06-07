<script>
export default {
    methods: {
        newTodo: function (e) {
            const newName = e.target.value.trim();
            if (newName) {
                this.$emit('new-todo', e.target.value);
                e.target.value = '';
            }
        },
		toggleAll: function () {
			this.$emit('toggled-all')
		},
    },
}
</script>

<template>
    <div class="todo-input-container">
		<button class="toggle-all-btn" @click="toggleAll"><label>❯</label></button>
        <input type="text" @keyup.enter="newTodo" placeholder="What needs to be done?">
    </div>
</template>

<style scoped>
.todo-input-container {
	position: relative;
	z-index: 1;
    display: flex;
}
.toggle-all-btn {
	font-size: 1.4rem;
    background-color: var(--color-panel-main);
    padding-inline: 10px;
}
.toggle-all-btn:focus {
    box-shadow: 0px 0px 5px 2px var(--color-highlight-main);
}
.toggle-all-btn label {
    writing-mode: vertical-lr;
}
.todo-input-container input[type="text"] {
    font-size: 1.4rem;
    padding: 16px;
    flex-grow: 1;
}
</style>
