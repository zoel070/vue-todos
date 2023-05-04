<template>
    <div class="main">
        <input id="toggle-all" class="toggle-all" type="checkbox" v-model="allCompleted">
        <label for="toggle-all">Mark all as complete</label>
        <ul class="todo-list">
            <li :class="['todo', { completed: todo.completed },
                    { editing: editTodo === todo }]" v-for="(todo) in showTodos" :key="todo.title">
                <div class="view">
                    <input class="toggle" type="checkbox" v-model="todo.completed" />
                    <label @dblclick="handleEdit(todo)">{{ todo.title }}</label>
                    <button class="destroy" @click="deleteTodo(todo)"></button>
                </div>
                <input class="edit" type="text" v-model="todo.title" v-todo-focus="editTodo === todo"
                    @blur="handleEditDone(todo)" @keyup.enter="handleEditDone(todo)" @keyup.esc="handleEditCancel(todo)" />
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        todos: {
            type: Array,
            default: () => []
        },
        select: {
            type: String,
            default: 'all'
        }
    },
    data() {
        return {
            editTodo: null,
            beforeEditCache: '',
        }
    },
    computed: {
        allCompleted: {
            get: function () { //被动计算的
                return this.todos.every(data => data.completed);
            },
            set: function (value) {  //主动传进来的，value是v-model里赋予的
                let todos = [...this.todos];//浅拷贝
                todos.forEach(data => data.completed = value);
                this.$emit('update:todos', todos);
            }
        },
        showTodos() {
            if (this.select == 'all') {
                return this.todos
            } else if (this.select == 'active') {
                return this.todos.filter(data => !data.completed)
            } else {
                return this.todos.filter(data => data.completed)
            }
        }
    },
    methods: {
        handleEdit(todo) {
            this.editTodo = todo;
            this.beforeEditCache = todo.title;
        },
        handleEditDone(todo) {
            if (todo.title.trim()) {
                this.editTodo = null;
                this.beforeEditCache = null;
            }
        },
        handleEditCancel(todo) {
            todo.title = this.beforeEditCache;
            this.editTodo = null;
            this.beforeEditCache = null;
        },
        deleteTodo(todo) {
            let index = this.todos.indexOf(todo);
            let todos = [...this.todos];//浅拷贝
            todos.splice(index, 1)
            this.$emit('update:todos', todos);
        },
    },
    directives: {
        'todo-focus': function (el, binding) {
            if (binding.value) {
                el.focus()
            }
        }
    }
}
</script>

<style></style>