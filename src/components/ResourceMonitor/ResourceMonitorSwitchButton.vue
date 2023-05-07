<script setup lang="ts">
 const emit = defineEmits(['click'])
 const prop = defineProps(['value', 'active'])
</script>

<template>
    <span :class="`rm-menu-side-item rm-btn ` + (prop.active ? `rm-btn-active`: ``)" @click="e => emit('click', e)">{{value}}</span>
</template>

<style scoped>

</style>