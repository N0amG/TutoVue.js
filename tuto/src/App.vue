<template id="todolist">
hello
</template>

<script setup>
import { ref } from 'vue'

const createTask = (value) => ref({
  title: value,
  done: false,
  date: new Date()
})

const task = createTask('Sample Task')


</script>

<style>

</style>