<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
 

   
  <header>
    
      
      <RouterLink class="text-white font-bold hover:text-white pr-2 pl-2" to="/">Vendas & Recebimentos</RouterLink>
      <RouterLink class="text-white font-bold hover:text-white pr-2 pl-2" to="/about">Consultas</RouterLink>



    
  </header>
  
  <RouterView class="mt-5"/>
</template>

<style scoped>
  @import 'assets/main.css';
  @import './assets/consultas/tableFinds.css';

header {
  line-height: 5;
  max-height: 100vh;
  background-color: rgb(233, 31, 169);
}

@media (min-width: 1024px) {
  header {
    display: flex;
    align-items: start; /* Ajuste para o eixo transversal */
    justify-content: start; /* Alinhar os elementos à esquerda */
    position: fixed; /* Fixar o cabeçalho no topo da página */
    width: 100%;
    top: 0;
    left: 0;
    z-index: 1000; /* Certifique-se de que o cabeçalho esteja acima de outros elementos */
  }

  .estilos {
    text-decoration-color: chocolate;

  }



}
</style>
