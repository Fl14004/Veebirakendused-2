<script setup>
defineProps(['items', 'title']);
</script>

<template>
    <section class="mb-5">
        <h2>{{ title }}</h2>
        <ul>
            <li v-for="item in items" :key="item.id"
                class="shopping-item"
                :class="'importance-' + item.importance">
                <label>
                    <input type="checkbox" v-model="item.isDone">
                    <span :class="{ completed: item.isDone }">{{ item.text }}</span>
                </label>
                <small>{{ item.importance }}</small>
            </li>
        </ul>
    </section>
</template>

<style scoped>
.shopping-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 12px;
    padding: 9px 12px;
    margin-bottom: 6px;
    border-radius: 6px;
}
.shopping-item label { display: flex; align-items: center; gap: 10px; }
.importance-kõrge { background-color: #ffc9c9; }
.importance-keskmine { background-color: #fff0b3; }
.importance-madal { background-color: #c9f0d0; }
.completed { text-decoration: line-through; }
</style>
