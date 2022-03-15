<template>
  <q-page class="row bg-grey-2">
    <transition
      enter-active-class="animated fadeIn"
      leave-active-class="animated fadeOut"
      mode="out-in"
    >
      <!-- EXIBE UM TEMPLATE CASO ESTEJA CARREGANDO -->
      <template v-if="loading">
        <div class="col flex flex-center">
          <div class="text-center">
            <q-spinner color="primary" size="55px"></q-spinner>
            <div class="text-primary q-mt-md">Carregando...</div>
          </div>
        </div>
      </template>
      <!-- DEPOIS QUE CARREGAR, EXIBE OUTRO TEMPLATE -->
      <template v-else>
        <q-scroll-area class="col">
          <div class="q-col-gutter-md row q-px-md q-pb-md pokemon-list-wrapper">
            <!-- ESSA DIV POSSUI UM LAÇO V-FOR, CRIARÁ UMA DIV PARA CADA ITEM EM POKEMONLIST -->
            <div
              class="col-12 col-md-3"
              v-for="pokemon in pokemonList"
              :key="pokemon.name"
            >
              <div class="bg-white q-pa-md rounded shadow-1">
                <div class="text-bold">Nome:</div>
                <div>
                  {{ pokemon.name }}
                </div>
                <div class="text-bold q-mt-md">URL:</div>
                <div class="ellipsis">
                  {{ pokemon.url }}
                </div>
              </div>
            </div>
          </div>
        </q-scroll-area>
      </template>
    </transition>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageIndex",

  // Prepara as variáveis que serão utilizadas dentro do componente
  data() {
    return {
      loading: true,
      pokemonList: [],
    };
  },

  // Essa função é executada assim que o componente é montado na tela
  mounted() {
    // faz uma chamada para a API de pokemon para carregar a lista
    this.$axios({
      method: "GET",
      url: "https://pokeapi.co/api/v2/pokemon",
    })
      // É chamado caso a chamada tenha sido bem sucedida
      .then((resp) => {
        // Pode olhar no console para ver o resultado da chamada
        console.log(resp);
        this.pokemonList = resp?.data?.results ?? [];
      })
      // É chamado caso a chamada tenha retornado um erro
      .catch((error) => {
        console.error(error);
      })
      // É chamado sempre, independente da chamada ter dado certo ou não
      .finally(() => {
        this.loading = false;
      });
  },
});
</script>

<style>
.pokemon-list-wrapper {
  max-width: 1000px;
  margin: 0px auto;
}
</style>