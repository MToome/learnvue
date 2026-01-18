<script setup>
import { ref } from 'vue';

    let message = ref('Hello, Vue!');

    function model(event){
        console.log(event);
        message.value = event.target.value;
    }
</script>

<template>
    <div class="container content mt-5">
        <!-- v-on:click="" juttumärkide vahele saame kirjutada javascripti koodi -->
        <!-- <button class="button is-primary" v-on:click=" message='Hello'">Click me</button> -->
        <!--  v-on: saab asendada @ -->
        <button class="button is-primary" @click=" message='Hello'">Click me</button>
        <!-- v-bind:value="" v-bind: võimaldab kasutada javascripti koodi   -->
        <!-- <input class="input" v-bind:value="message"> -->
        <!-- v-bind: saab asendada lihtsalt : , väärtuse jaoks -->
        <!-- <input class="input" :value="message" @input="message = $event.target.value"> -->
         <!-- :value="message" @input="message = $event.target.value" saab asendada v-model="message" -->
        <input class="input" v-model="message">
        <h1>{{ message.split('').reverse().join('') }}</h1>
    </div>
</template>