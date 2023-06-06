<template>
    <ul class="list-group rounded-0">
        <div v-for="(assignment, index) in assignments" :key="index">
            <Assignment :assignment="assignment" v-on:assignmentchanged="emit('reloadList')"></Assignment>
        </div>
    </ul>
</template>
<script setup>
import Assignment from './Assignment.vue';
const props = defineProps(['assignments'])
const emit = defineEmits(['reloadList'])

</script>