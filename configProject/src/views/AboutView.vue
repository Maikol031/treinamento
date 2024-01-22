<template>
  
  <div class="flex justify-center  mb-1">
    <div class="flex flex-col">
      <label for="dataI" class="font-bold pl-5">Data inicial</label>
      <input type="date" v-model="dataI" class="border border-gray-900 rounded-sm mr-3">
    </div>
    <div class="flex flex-col">
      <label for="dataF" class="font-bold pl-5">Data final</label>
      <input type="date" class="border border-gray-900 rounded-sm" v-model="dataF">
    </div>
    <button class="bg-pink-400 ml-2 px-5 h-6 mt-[24px] rounded-md text-white hover:bg-pink-500 hover:scale-110" @click="getList()">Filtrar</button>
  </div>
   <div class="table-title">
     <label class="border border-x-black  bg-gray-300 font-bold pl-7 pr-5" for="Método">Método</label>
     <label class="border border-x-black  bg-gray-300 font-bold pl-7 pr-5" for="Bandeira">Bandeira</label>
     <label class="border border-x-black  bg-gray-300 font-bold pl-7" for="Tipo">Tipo</label>
     <label class="border border-x-black  bg-gray-300 font-bold" for="Nº Parcelas">Nº Parcelas</label>
     <label class="border border-x-black  bg-gray-300 font-bold" for="Valor">Valor</label>
     <label class="border border-x-black  bg-gray-300 font-bold" for="Valor Liquído">Valor Liquído</label>
     <label class="border border-x-black  bg-gray-300 font-bold pl-7" for="Data">Data</label>
     <label class="border border-x-black  bg-gray-300 font-bold pl-7" for="Excluir">Excluir</label>
   </div>
   <div v-if="datas.length" class="table-title" v-for="dados in datas">
     <label class="border border-x-gray-400 pl-7" for="Método">{{ dados.metodo.nome}}</label>
     <label class="border border-x-gray-400 pl-5" for="Bandeira">{{ dados.bandeiras.nome}}</label>
     <label class="border border-x-gray-400 pl-1" for="Tipo">{{ dados.tipo.nome }}</label>
     <label class="border border-x-gray-400" for="parcelas">{{ dados.parcelas }}</label>
     <label class="border border-x-gray-400" for="valorBruto">{{ dados.valorbr }}</label>
     <label class="border border-x-gray-400" for="valorLiquido">{{ dados.valorlq }}</label>
     <label class="border border-x-gray-400" for="data">{{converterDataFormato(dados.data)}}</label>

     <button class=" w-fit ml-11  hover:scale-110" @click="deleteMany(dados.id)">
       <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash hover:w-17" viewBox="0 0 16 16">
           <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0z"/>
           <path d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4zM2.5 3h11V2h-11z"/>
         </svg>
     </button>

     
     
    </div>
    <div class="flex justify-center bg-gray-200 border border-gray-700 px-2 hover:bg-gray-300" @click="openDetail()">
         <label>{{ 'Detalhes ' }}</label>
    </div>

    <div v-if="showDetail">
      <div class="flex flex-col  bg-gray-200 border border-gray-700 px-2">
           <label>{{ 'Valor Total: ' }}{{ totalValue}}</label>
         </div>
         <div class="flex flex-col justify-center bg-gray-200 border border-gray-700 px-2">
           <label>{{ 'Valor Liquido Total: ' }}{{ totalValueLiquid }}</label>
      </div>
    </div>
    <div class="flex justify-between pt-2">
       <button class="btn-style" @click="alterPageAnt()">Página Anterior</button>
       <button class="btn-style" @click="alterPageProx()">Proxima Página</button>
   
    </div>


</template>
 
<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';
import dayjs from 'dayjs';

const dataI = ref()
const dataF = ref()
const datas = ref([])
const pag = ref(0)
const pages = ref()
const showDetail = ref(false)
const totalValue = ref(0)
const totalValueLiquid = ref(0)
const values = ref([])


const alterPageAnt = () => {
  if(pag.value > 0) pag.value--
  getList()
  
}

const alterPageProx = () => {
  if(pag.value < pages.value.totalPages - 1) pag.value++
  getList()
}


const openDetail = () => {
  showDetail.value = !showDetail.value;

}


const getList = async() => {

  const startDate = dayjs(dataI.value)
  const endDate = dayjs(dataF.value)
  
  const inicialFormatDate = startDate.format("YYYY-MM-DDT00:00:00");
  const finallyFormatDate = endDate.format("YYYY-MM-DDT23:59")
  
  try {
    let {data} = await axios({
      url: `http://localhost:8080/operacoes/datas/${pag.value}?datai=${inicialFormatDate}&dataf=${finallyFormatDate}`,
      method: "GET",
  
    })
  
    datas.value = data.content
    pages.value = data

    totalValue.value = datas.value.reduce((accumulator, currentValue) => accumulator + currentValue.valorbr, 0);
    totalValueLiquid.value = datas.value.reduce((accumulator, currentValue) => accumulator + currentValue.valorlq, 0);
   

  } catch (error) {
    console.error(error)
  }
}


const deleteMany = async(id) => {
  try {
    await axios({url:`http://localhost:8080/operacoes/${id}`,
                method: 'DELETE'})
  }catch (error) {
    console.error(error)
  }finally{
    getList()

  }


}



onMounted(() => {
  getList()
 
})




function converterDataFormato(dataString) {

    var data = new Date(dataString);

    if (!isNaN(dataString)) {
        return "Data inválida";
    }
    // Extrair dia, mês e ano
    var dia = data.getDate();
    var mes = data.getMonth() + 1; // Os meses começam do zero, então adicionamos 1
    var ano = data.getFullYear();


    // Formatando para DD-MM-AAAA
    var dataFormatada = (dia < 10 ? '0' : '') + dia + '-' + (mes < 10 ? '0' : '') + mes + '-' + ano;

    return dataFormatada;
}

</script>

<style scoped>


@media (min-width: 1024px) {
  .about {
    display: inline-flex;
    padding-bottom: 0%;
    margin-bottom: 0%;
    
  }

}

.table-title {
  @apply grid grid-cols-8 border border-black



}

.btn-style{
  @apply bg-pink-400 px-5 rounded-md text-white font-medium hover:bg-pink-500 m-1 hover:transition-all hover:scale-110 duration-300;

}




</style>
