<template>
    <div class="mt-5">
<li v-for="todo in props.todos" :key="todo">
    <span class="text-lg ">{{ todo.text }}</span>
</li>
    </div>
</template>
<script setup>

const props=defineProps(['todos'])

</script>