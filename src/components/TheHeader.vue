<template>
    <div class="header">
        <h1>todos</h1>
        <input class="new-todo" autofocus v-model="newTodo" @keyup.enter="addTodo" autocomplete="off"
            placeholder="What needs to be done?">
    </div>
</template>

<script>


export default {
    data() {
        return {
            newTodo: '',
        }
    },
    methods: {
        addTodo() {
            if (this.newTodo.trim()) {
                this.$emit('addTodo', this.newTodo);
                this.newTodo = '';
            }
        },
    }
}
</script>

<style></style>