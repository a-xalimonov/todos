<script>
import PageListItem from './PageListItem.vue';

export default {
    components: {
        PageListItem,
    },
    props: {
        pages: Array,
        selected: Number,
    },
};
</script>

<template>
    <div class="page-selector-container">
        <PageListItem v-for="(page, index) in pages" :key="index" :page="page" :isActive="page === pages[selected]" />
        <button @click="$emit('page-added')">+</button>
    </div>
</template>

<style scoped>
.page-selector-container {
    width: 100%;
    display: flex;
}

.page-selector-container>button {
    font-size: 1.6rem;
    margin-left: 6px;
}
</style>
