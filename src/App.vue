<template  >
  <div v-bind:class="myClass" class="final">
  <div class="app" >
    <h1>Jogo da Velha</h1>

      <section id="inicio" v-if="tela === 'inicio'">
        <FormularioPage v-if="etapa === 'palavra'"
          title="Defina a Palavra"
          button="Próximo"
          :action="setPalavra"
        />
        <FormularioPage v-if="etapa === 'dica'"
          title="Defina a Dica"
          button="Iniciar Jogo :)"
          :action="setDica"
        />
      </section>

      <section id='jogo' v-if="tela === 'jogo'">
        <JogoPage
        :erros = "erros"
        :palavra_digitada = "palavra_digitada"
        :dica_digitada = "dica_digitada"
        :verificaLetra = "verificaLetra"
        :etapa = "etapa"
        :letras = "letras"
        :jogar = "jogar"
        />
      </section>


      <section class='final' v-if="etapa === 'ganhador'">
        <div>parabéns você ganhou!!!!!</div>
        <a href="" class="button">Novo jogo</a>
      </section>

      <section class='final' v-if="etapa === 'enforcado'">
        <div>Opsss!!!!! Você foi enforcado</div>
        <a href="" class="button">Novo jogo</a>
      </section>


  </div>
</div>
</template>

<script setup>
import '@/css/global.css'
import { ref } from 'vue'
import FormularioPage from '@/components/formularioPage.vue'
import JogoPage from '@/components/jogoPage.vue'


const tela = ref('inicio')
const etapa = ref('palavra')
const palavra_digitada = ref('')
const dica_digitada = ref('')
const erros = ref(0)
const letras = ref([])
const myClass = ref()

const setPalavra = (palavra) => {
  palavra_digitada.value = palavra.trim()
  etapa.value = 'dica'
}

const setDica = (dica) => {
  dica_digitada.value = dica
  etapa.value = 'jogo'
  tela.value = 'jogo'
}

const verificaLetra = (letra) => {
  return letras.value.find(item => item.toLowerCase() === letra.toLowerCase() )
}

const jogar = (letra) => {
  //Adiciona Letra jogada
  letras.value.push(letra)

  //validar Erro
  verificarErros(letra)
}

const verificarErros = (letra) => {
  //acerto
  if(palavra_digitada.value.toLowerCase().indexOf(letra.toLowerCase()) >= 0){
    return verificarAcertos()
  }
  //erros
  erros.value++;

  //enforcado
  if(erros.value === 6){
    etapa.value = 'enforcado'
    myClass.value = 'enforcado'
  }

}

const verificarAcertos = () => {
  let letrasUnicas = [...new Set(palavra_digitada.value.split('') ) ]
  if(letrasUnicas.length == (letras.value.length - erros.value) ){
    etapa.value = 'ganhador'
    myClass.value = 'ganhador'
  }

}

</script>

<style>
#app {
  width: 100%;
  height: 100%;
  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}


.final{
  font-size: 20px;

  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
}


.enforcado{

  background-color: var(--color-text-error);
}

.ganhador{

  background-color: var(--color-text-success);
}

.button{
  margin-top: 20px;
}
</style>
