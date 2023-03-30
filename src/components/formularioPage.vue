<template>
    <div class='formulary'>
        <div class='formulary-title'>
            {{ props.title }}
        </div>
        <input type="text" class="formulary-input" v-model="inputValue">
        <button v-on:click="onSubmit" :disabled="inputValue.length === 0">{{ props.button }}</button>
    </div>
</template>

<script setup>
import { defineProps, ref } from 'vue'

const props = defineProps({
  title: String,
  button: String,
  action:Function
})

const inputValue = ref('')

function onSubmit() {
  props.action(inputValue.value)
  inputValue.value = ''
}

</script>

<style>
    .formulary{
        display:flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        justify-content: center;
        margin-top: 20px;
    }

    .formulary-input{
        padding: 10px 5px;
        border:0;
        border-radius: 5px;
        margin:10px 0px;
        text-align: center;
        color:var(--color-text-dark);
        font-size: 16px;
    }
</style>
