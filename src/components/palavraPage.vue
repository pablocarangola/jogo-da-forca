<template>
    <div class='palavra'>
        <div class="palavra_letas">
        <div class="palavra_letra" v-for="(letra, key) in props.palavra_digitada" :key="key">
            {{ ( verificaLetra(letra) || etapa === 'enforcado') ? letra : '' }}
        </div>
        </div>

        <div class="palavra_dica"> {{ props.dica_digitada }} </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    palavra_digitada: String,
    dica_digitada: String,
    verificaLetra: Function,
    etapa: String
})

</script>

<style>

.palavra{
    text-transform: uppercase;
    display: flex;
    flex-direction: column;
    text-align: center;
    align-items: center;
}

.palavra_letas{
    display: flex;
    margin-bottom: 20px;
}

.palavra_letra{
    height: 30px;
    width: 30px;
    margin: 0 5px;
    border-bottom: 1px solid var(--color-text-light);
    display:flex;
    justify-content: center;
    align-items: center;
}

</style>
