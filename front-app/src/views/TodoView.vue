<template>
    <div class="todo">
        <h1>TODO APP</h1>
        <div class="crate">
            <div class="title">
                <label for="">title:</label>
                <input v-model="state.title" type="text">
                <button @click="createTodo">Create</button>
            </div>
        </div>
        <div v-for="todo in state.todos" :key="todo.uuid">
            <input class="margin-r1" v-model="todo.title" />
            <select class="margin-r1" v-model="todo.status">
                <option value="todo">TODO</option>
                <option value="wip">WIP</option>
                <option value="done">DONE</option>
            </select>
            <button class="update margin-r1" @click="updateTodo(todo)">Update</button>
            <button class="delete margin-r1" @click="deleteTodo(todo)">Delete</button>
        </div>
    </div>
</template>
  
<script lang="ts">
import { defineComponent, reactive } from 'vue';
import axios from 'axios';

const baseURL = 'http://localhost:3000/';

type Todo = {
    uuid: string;
    title: string;
    status: 'todo' | 'wip' | 'done';
};


export default defineComponent({
    name: 'TodoView',
    setup() {
        const state = reactive({
            title: '',
            todos: null,
        });

        const getTodos = () => {
            axios.get(baseURL).then((res) => {
                if (res && res.data) {
                    console.log(res);
                    state.todos = res.data.resBody;
                }
            });
        };

        getTodos();

        const createTodo = async () => {
            await axios.put(baseURL, { title: state.title });
            getTodos();
        };

        const updateTodo = async (todo: Todo) => {
            await axios.post(baseURL + todo.uuid, {
                title: todo.title,
                status: todo.status,
            });
            getTodos();
        };

        const deleteTodo = async (todo: Todo) => {
            await axios.delete(baseURL + todo.uuid);
            getTodos();
        };

        return {
            state,
            createTodo,
            updateTodo,
            deleteTodo,
        };
    },
});
</script>

<style lang="scss" scoped>
.todo-item {
    display: flex;
    justify-content: center;

    .margin-r1 {
        margin-right: 1rem;
    }
}
</style>