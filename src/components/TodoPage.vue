<script>
export default {
    data: function () {
        return {
            isEdited: false,
        }
    },
    props: [
        'page', 'isActive'
    ],
    inject: [
        'selectPage',
        'renamePage',
        'deletePage'
    ],
    methods: {
        startEdit: function () {
            const width = this.$refs.pageName.clientWidth;
            this.isEdited = true;
            this.$nextTick(() => {
                this.$refs.pageNameInput.style.width = width + 'px';
                this.$refs.pageNameInput.focus()
            })
        },
        stopEdit: function (e) {
            this.isEdited = false;
            const newName = e.target.value.trim();
            if (newName) {
                this.renamePage(this.page, e.target.value);
            }

        }
    }
}
</script>

<template>
    <div class="todo-page" :class="{ selected: this.isActive }">
        <div v-show="!isEdited" ref="pageName" @click="selectPage(page)" @dblclick="startEdit">
            <label v-if="!isEdited">{{ page.name }}</label>
            <button v-show="isActive" class="delete-page-btn" @click="deletePage(page)">×</button>
        </div>
        <input v-show="isEdited" ref="pageNameInput" type="text" @keyup.enter="stopEdit" @blur="stopEdit"
            :value="page.name">
    </div>
</template>

<style scoped>
.todo-page {
    background-color: var(--color-panel-dark);
    margin-right: 4px;
    overflow: hidden;
    text-wrap: nowrap;
}

.selected {
    background-color: var(--color-panel-main);
    box-shadow: 0px 0px 20px 0px #0000003d;
    position: relative;
    overflow: visible;
}

.todo-page>* {
    font-size: 1rem;
    padding: 0.5rem;
}
label {
    margin-right: 1.4rem;
}

.delete-page-btn {
    position: absolute;
    right: 0.5rem;
    top: 50%;
    line-height: 0;
    font-size: 1.6rem;
}
</style>
