<template>
    <div class="wrapper">
        <div class="count"> {{ count }}</div>
        <div class="label"> {{ label }}</div>
    </div>    
</template>

<script setup lang="ts">
    defineProps<{  count: string, label: string }>()
</script>

<style scoped>

.count{
    font-size: 4rem;
    font-weight: 800;
}

.wrapper{
    color: rgb(221, 15, 94);
    text-align: center;
}
</style>