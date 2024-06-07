<script>
import TodoPage from './TodoPage.vue';

export default {
    components: {
        TodoPage,
    },
    props: ['pages', 'selected'],
};
</script>

<template>
    <div class="page-selector-container">
        <TodoPage v-for="page in pages" :page="page" :isActive="page === pages[selected]"/>
        <button @click="$emit('page-added')">+</button>
    </div>
</template>

<style scoped>
.page-selector-container {
    width: 100%;
    display: flex;
}
.page-selector-container > button {
    font-size: 1.6rem;
    margin-left: 6px;
}
</style>
