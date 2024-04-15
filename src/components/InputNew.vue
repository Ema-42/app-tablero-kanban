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
        <input class="input-new" type="text" v-model="text" placeholder="Nuevo Item">
    </form>
</template>
<style scoped>
.input-new{
    height: 25px;
    margin-bottom: 10px;
    margin-top: 5px;
    font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
    font-size: 16px;
    border: 1px solid rgb(207, 207, 207);
    border-radius: 5px;
    background-color: #dddddc;
}
</style>

