<script setup>
import {ref} from 'vue'
import Select2 from 'vue3-select2-component'

const cats = ref([{id: 'foo', text: 'Foo'}, {id: 'bar', text: 'Bar'}])
const selected_cat = ref('')
</script>


<template>
    <h1>Vue 3 + Vite + Select2</h1>

    <Select2 id="selected_cat" v-model="selected_cat" :options="cats" :settings="{ width: '300px' }"/>
</template>


<style>
#app {font-family: Avenir, Helvetica, Arial, sans-serif;-webkit-font-smoothing: antialiased;-moz-osx-font-smoothing: grayscale;text-align: center;color: #2c3e50;margin-top: 60px;}
</style>
