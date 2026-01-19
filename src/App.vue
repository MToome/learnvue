<script setup>
import { ref, computed } from 'vue';
import ItemList from './ItemList.vue';

// bulma message example
let message = ref('Hello, Vue!');

function model(event) {
    console.log(event);
    message.value = event.target.value;
}

// bulm field example
let newItem = ref('');
let i = 1;
let items = ref([
    { id: i++, name: 'Sai', isDone: false },
    { id: i++, name: 'Piim', isDone: true },
    { id: i++, name: 'Muna', isDone: false },
]);

function addItem() {
    if (newItem.value.trim() !== '') {
        items.value.push({ id: i++, name: newItem.value.trim(), isDone: false });
        newItem.value = '';
    }
}

let doneItems = computed(()=> items.value.filter(item=> item.isDone));
let todoItems = computed(()=> items.value.filter(item=> !item.isDone));
</script>

<template>
    <!-- Bulma message example  -->
    <div class="container is-fluid content mt-5">
        <!-- v-on:click="" juttumärkide vahele saame kirjutada javascripti koodi -->
        <!-- <button class="button is-primary" v-on:click=" message='Hello'">Click me</button> -->
        <!--  v-on: saab asendada @ -->
        <button class="button is-primary" @click=" message = 'Hello'">Click me</button>
        <!-- v-bind:value="" v-bind: võimaldab kasutada javascripti koodi   -->
        <!-- <input class="input" v-bind:value="message"> -->
        <!-- v-bind: saab asendada lihtsalt : , väärtuse jaoks -->
        <!-- <input class="input" :value="message" @input="message = $event.target.value"> -->
        <!-- :value="message" @input="message = $event.target.value" saab asendada v-model="message" -->
        <input class="input" v-model="message">
        <h1>{{ message.split('').reverse().join('') }}</h1>
    </div>

    <!-- Bulma field example -->
    <div class="container is-fluid content mt-5">
        <div class="field is-fluid ml-5 has-addons">
            <div class="control is-expanded">
                <input @keydown.enter="addItem" v-model="newItem" class="input" type="text" placeholder="Add item">
            </div>
            <div class="control">
                <button class="button is-info" @click="addItem">
                    item
                </button>
            </div>
        </div>

        <ItemList :items="items" title="All items"></ItemList>
        <ItemList :items="doneItems" title="Done items"></ItemList>
        <ItemList :items="todoItems" title="ToDo items"></ItemList>

    </div>
</template>