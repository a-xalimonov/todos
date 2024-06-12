<script>
export default {
    props: {
        value: String,
    },
};
</script>

<template>
    <div class="todo-filter">
        <label @click="$emit('input', 'all')" :class="{ selected: value === 'all' }">All</label>
        <label @click="$emit('input', 'active')" :class="{ selected: value === 'active' }">Active</label>
        <label @click="$emit('input', 'completed')" :class="{ selected: value === 'completed' }">Completed</label>
    </div>
</template>

<style scoped>
.todo-filter {
    display: inline-block;
}

.todo-filter label {
    padding: 0.3rem;
    border: solid 1px transparent;
    border-radius: 5px;
    margin-inline: 0.2rem;
}

.todo-filter label:hover {
    border-color: var(--color-highlight-main);
    cursor: pointer;
}

.todo-filter label.selected {
    border-color: var(--color-highlight-main);
    box-shadow: 0px 0px 4px 0px var(--color-highlight-main);
}</style>
