<template>
    <div>
<li v-for="todo in props.todos" :key="todo">
    <span>{{ todo.text }}</span>
</li>
    </div>
</template>
<script setup>

const props=defineProps(['todos'])

</script>