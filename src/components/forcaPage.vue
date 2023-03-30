<template>
    <div class='forca'>
        <img alt="Erro Forca" :src="`https://raw.githubusercontent.com/william-costa/wdev-hangman-game-resources/master/images/hangman/${props.erros}.svg`">
    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    erros: Number
})

</script>

<style>

.forca img{
    height:200px ;
}

</style>
