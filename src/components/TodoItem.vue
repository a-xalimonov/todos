<script>

export default {
    props: ['item'],
    inject: ['deleteTodo', 'toggleTodo', 'renameTodo'],
    data: function () {
        return {
            isEdited: false,
        }
    },
    methods: {
        startEdit: function () {
            this.isEdited = true;
            this.$nextTick(() =>
                this.$refs.itemNameInput.focus()
            )
        },
        stopEdit: function (e) {
            this.isEdited = false;
            const newName = e.target.value.trim();
            if (newName) {
                this.renameTodo(this.item, e.target.value);
            }
        },
    },
}
</script>

<template>
    <li class="class-item">
        <div v-show="!isEdited" @dblclick="startEdit">
            <label class="custom-checkbox" :class="{ completed: item.completed }">
                <input type="checkbox" @change="toggleTodo(item)" :checked="item.completed">
            </label>
            
            <label class="todo-label" :class="{ completed: item.completed }">{{ item.name }}</label>
            <button class="delete-todo-btn" @click="deleteTodo(item)">×</button>
        </div>
        <input type="text" v-show="isEdited" ref="itemNameInput" :value="item.name" @keyup.enter="stopEdit"
            @blur="stopEdit">
    </li>
</template>

<style scoped>
.custom-checkbox {
    display: inline-block;
    position: absolute;
    left: 10px;
    box-sizing: border-box;
    border: solid 1px var(--color-checkmark-inactive);
    width: 30px;
    height: 30px;
    border-radius: 15px;
    background-repeat: no-repeat;
    background-position: center;
    margin-right: 26px;
    flex-shrink: 0;
}
.custom-checkbox.completed {
    background-image: url('../assets/checkmark.svg');
    border-color: var(--color-checkmark-active);
}

input[type="checkbox"] {
    position: absolute;
    z-index: -1;
    opacity: 0;
}

.class-item {
    border-top: solid 1px var(--color-background);
    position: relative;
}

.class-item > * {
    padding: 10px 10px 10px 66px;
    font-size: 1.4rem;
}

.todo-label {
    word-break: break-all;
}

.todo-label.completed {
    text-decoration: line-through;
    color: var(--color-text-light)
}

.class-item > div {
    height: 100%;
    display: flex;
    align-items: center;
}

.delete-todo-btn {
    position: absolute;
    right: 10px;
    display: none;
    font-size: 2.4rem;
    line-height: 1.4rem;
    margin-left: auto;
}

li:hover .delete-todo-btn {
    display: inline;
}

input[type="text"] {
    height: 100%;
    width: 100%;
}
</style>
