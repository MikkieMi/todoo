<script setup>
import {reactive, ref, watch} from "vue";

const newItem = ref('')
const items = reactive(JSON.parse(localStorage.getItem('todo-items') || '[]'))

watch(items, (value) => {
    localStorage.setItem('todo-items', JSON.stringify(value))
})

const addItem = () => {
    if (newItem.value.trim() !== '') {
        items.unshift(newItem.value)
        newItem.value = ''
    }
}

const removeItem = (index) => {
    items.splice(index, 1)
}
</script>

<template>
<div class="container-fluid d-flex flex-column bg-primary min-vh-100">
    <div class="row bg-white mt-5 mx-3 mb-auto p-3 rounded">
        <div class="col">
            <div class="text-center mb-4">
                <h1 class="mb-2">Todo List</h1>
                <p class="text-muted mb-0">Add tasks and remove them when they are done.</p>
            </div>

            <div class="d-flex my-4">
                <input v-model="newItem" @keyup.enter="addItem" type="text" class="form-control me-3" placeholder="Enter a task">
                <button @click="addItem" class="btn btn-success px-4">Add</button>
            </div>

            <div v-for="(item, index) in items" :key="index" class="alert alert-secondary fade show d-flex align-items-center justify-content-between mt-3 px-3 py-2">
                <span>{{ item }}</span>
                <button @click="removeItem(index)" type="button" class="btn btn-danger">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="24" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
                        <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0z"/>
                        <path d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4zM2.5 3h11V2h-11z"/>
                    </svg>
                </button>
            </div>
            <div v-if="items.length === 0">
                No tasks yet. Add one!
            </div>
        </div>
    </div>
</div>
</template>

<style scoped>

</style>