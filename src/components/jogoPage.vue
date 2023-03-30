<template>
    <div class='play'>
      <ForcaPage
        :erros =  "props.erros"
      />

      <PalavraPage
        :palavra_digitada = "props.palavra_digitada"
        :dica_digitada = "props.dica_digitada"
        :verificaLetra = "props.verificaLetra"
        :etapa = "props.etapa"
      />

      <TecladoPage
      :letras = props.letras
      :verificarLetra="props.verificaLetra"
      :jogar = "props.jogar"
      v-if="props.etapa == 'jogo'"
      />

    </div>
</template>

<script setup>
import { defineProps } from 'vue'
import ForcaPage from '@/components/forcaPage.vue'
import PalavraPage from '@/components/palavraPage.vue'
import TecladoPage from '@/components/tecladoPage.vue'

const props = defineProps({
  erros: Number,
  palavra_digitada: String,
  dica_digitada: String,
  verificaLetra: Function,
  etapa: String,
  letras: Array,
  jogar: Function
})

</script>

<style>
  .play{
    width: 100%;
    display:flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

</style>
