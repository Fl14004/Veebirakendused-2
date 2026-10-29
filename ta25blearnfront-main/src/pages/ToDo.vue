<script setup>
import { computed, ref } from 'vue';
import ItemList from '../components/ItemList.vue';

const message = ref('');
const importance = ref('keskmine');
let i = 1;
const items = ref([
    { id: i++, text: 'Piim', isDone: false, importance: 'kõrge' },
    { id: i++, text: 'Viin', isDone: true, importance: 'madal' },
    { id: i++, text: 'Õlu', isDone: false, importance: 'keskmine' },
    { id: i++, text: 'Sai', isDone: true, importance: 'kõrge' },
]);

const importanceOrder = { 'kõrge': 0, 'keskmine': 1, 'madal': 2 };

function add() {
    const text = message.value.trim();
    if (!text) return;
    items.value.push({
        id: i++,
        text,
        isDone: false,
        importance: importance.value,
    });
    message.value = '';
    importance.value = 'keskmine';
}

const sortedItems = computed(() =>
    [...items.value].sort((a, b) => importanceOrder[a.importance] - importanceOrder[b.importance])
);
const doneItems = computed(() => sortedItems.value.filter(item => item.isDone));
const toDoItems = computed(() => sortedItems.value.filter(item => !item.isDone));
</script>

<template>
    <div class="container content mt-2">
        <form class="field is-grouped is-align-items-center" @submit.prevent="add">
            <div class="control is-expanded">
                <input v-model="message" class="input" type="text" placeholder="Add item">
            </div>
            <div class="control">
                <div class="select">
                    <select v-model="importance" aria-label="Olulisus">
                        <option value="kõrge">Kõrge</option>
                        <option value="keskmine">Keskmine</option>
                        <option value="madal">Madal</option>
                    </select>
                </div>
            </div>
            <div class="control">
                <button type="submit" class="button is-info">Add</button>
            </div>
        </form>

        <ItemList :items="sortedItems" title="All items" />
        <ItemList :items="doneItems" title="Done items" />
        <ItemList :items="toDoItems" title="ToDo items" />
    </div>
</template>
