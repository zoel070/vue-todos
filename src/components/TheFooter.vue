<template>
    <div class="footer">
        <span class="todo-count">
            <strong>{{ todos.length }}</strong> todo
        </span>
        <ul class="filters">
            <li><a href="#/all" :class="{ selected: select == 'all' }" @click="handleChangeSelect('all')">All</a></li>
            <li><a href="#/active" :class="{ selected: select == 'active' }"
                    @click="handleChangeSelect('active')">Active</a></li>
            <li><a href="#/completed" :class="{ selected: select == 'completed' }"
                    @click="handleChangeSelect('completed')">Completed</a>
            </li>
        </ul>
        <button class="clear-completed" v-show="hasCompleted" @click="deleteDone">Clear completed</button>
    </div>
</template>

<script>
export default {
    props: {
        select: {
            type: String,
            default: 'all',
        },
        todos: {
            type: Array,
            default: () => [],
        }
    },
    computed: {
        hasCompleted() {
            return this.todos.some(data => data.completed)
        },
    },
    methods: {
        handleChangeSelect: function (value) {
            this.$emit('update:select', value);
        },
        deleteDone() {
            let todos = this.todos.filter(data => !data.completed)
            this.$emit('update:todos', todos)
        },
    },
}
</script>

<style></style>