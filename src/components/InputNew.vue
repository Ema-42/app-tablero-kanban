<script setup>
import {ref,defineEmits} from 'vue'
 
const text = ref('')
const emits = defineEmits(['onNewItem'])
const handleSubmit = () =>{
    if (text.value !== '') {
        //manda a llamar al emit
        emits('onNewItem',text)
        text.value = ''
    }
}
</script>
<template>
    <form @submit.prevent="handleSubmit">
        <input class="input-new" type="text" v-model="text" placeholder="Introducir Item">
    </form>
    <p class="input-mensaje">Presiona Enter para agrar el item.</p>
</template>
<style scoped>
.input-mensaje{
    font-size: 13px;
}
.input-new{
    height: 40px;
   
    margin-top: 5px;
    font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    background-color: #fff3ca;
    color: black;
    padding-left: 1rem
}
</style>

