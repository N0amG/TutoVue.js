<template id="todolist">
    <Layout>
        <template #header>
            <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.min.css">
            <h1>Todo List</h1>
        </template>

        <template #main>

            <div>
                <form action="" @submit.prevent="addTask">
                    <input type="text" placeholder="Ajouter une tâche" v-model="task.title">
                    <button type="submit">Add</button>
                </form>
            </div>
            <div v-show="tasks.length > 0">
                <ul>
                    <li v-for="task in sortedTasks" :key="task.date">
                        <Checkbox :label="task.title" v-model="task.done" />
                    </li>
                </ul>
            </div>
            <p v-if="remaingTasks > 0">{{ remaingTasks }} remaining tasks</p>
            <div v-show="tasks.length === 0">
                <p>No tasks</p>
            </div>
            <label>
                <input type="checkbox" v-model="hideDone">
                Hide completed tasks
            </label>
        </template>

    </Layout>
</template>

<script setup>
import { computed, ref } from 'vue'
import Checkbox from './Checkbox.vue'
import Button from './Button.vue'
import Layout from './Layout.vue'

const createTask = (value) => ({
    title: value,
    done: false,
    date: new Date()
})

const tasks = ref([]) // Array of tasks

const task = ref(createTask(''))

const hideDone = ref(false)

const addTask = () => {
    if (task.value.title.trim() !== '') {
        tasks.value.push(createTask(task.value.title))
        task.value.title = '' // Reset the input field
    }
}

const sortedTasks = computed(() => {
    console.log('sortedTasks')
    tasks.value = tasks.value.sort((a, b) => {
        if (a.done === b.done) {
            return a.date - b.date; // Trier par date si les deux tâches ont le même statut
        }
        return a.done ? 1 : -1; // Placer les tâches effectuées en bas
    });
    return tasks.value.filter(task => !hideDone.value || !task.done);
})

const remaingTasks = computed(() => tasks.value.filter(task => !task.done).length)

</script>

<style>
body {
    width: 90%;
    padding-left: 100px;
}

form {
    width: 90%;
}

.done {
    text-decoration: line-through;
    opacity: 0.5;
}
</style>