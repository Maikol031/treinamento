<template>
    <h1 class="font-bold shadow-lg text-9xl pl-8">Chibel Modas</h1>
    <div class="table-container-type font-styles !text-gray-600 flex justify-center pl-40 border-2 border-gray-500" > 
        <h1 class=" px-2 rounded-md w-fit" v-for="ids in array"> <input type="radio" v-model="registroModel.metodo.id"  name="TypeMethod" :value=" ids.id" @click="funcRadio(ids.id)" class="mr-2">{{ids.name}}</h1>
     

    </div>
    <div class="bg-pink-500 border-x-2 border-gray-500">
        <div class="table-container-cards font-styles pl-24">
    <label  for="Master-Card" class="px-2 rounded-md w-fit" v-for="cards in arrayCads">
        <input type="radio" v-model="registroModel.bandeiras.id" :disabled="radioPayMethod"  name="paymentMethod" :value="cards.id" class="mr-2">{{cards.name}}
    </label>

</div>
        <div class="table-container-type-payment font-styles flex justify-center" >
            <div v-for="typeV in typeSale">

                <input  type="radio" v-model="registroModel.tipo.id" :value="typeV.id" @click="verifyCheck1(typeV.id)" name="radioType" class="mr-2">{{typeV.name}}

            </div>
                
        </div>
    </div>
    <div class="border-2 border-gray-500 pb-2 pt-2">
        <div class="table-container font-styles !text-gray-600 flex justify-center ">
            <label for="numberVezes" class="w-fit !text-xs !font-bold">NºParcelas</label>
            <input type="number" min="1" v-model="registroModel.parcelas" max="12" class="w-20 border-2 border-gray-400">
            <input type="number" class="border-2 border-gray-400 w-20" v-model="registroModel.valorbr" placeholder="R$">
        </div>
        <div class="flex justify-center pt-2">
            <button  class=" bg-pink-500 px-3 py-2 font-bold !text-white hover:bg-pink-600  rounded-md shadow-xl transition ease-in-out delay-150 hover:-translate-y-1 hover:scale-110  duration-300 " :disabled="disabledButton" @click="addList()">Enviar</button>
        </div>
    </div>


</template>
<script setup>
import {onMounted, reactive, ref } from 'vue';
import axios from "axios"
// import paymentCards from '../model/PaymentCards'
import {registroPayments} from '../@model/registroVendas/registroPayments'


const radioPayMethod = ref(false)
const disabledButton = ref(true)
const registroModel = reactive(new registroPayments())

const array = ref([{name: 'Débito', id: 1}, {name: 'Crédito', id: 2}, {name: 'Pix', id: 3}])
const arrayCads = ref([{name: 'Master-Card', id: 1}, {name: 'Visa', id: 2}, {name: 'ELO', id: 3}, {name: 'HiperCard', id: 4}])
const typeSale = ref([{name: 'Vendas', id: 1}, {name: 'Recebimentos', id: 2}])


const funcRadio = (id) =>{
    console.log(radioPayMethod.value)
    if(id == 3){ radioPayMethod.value = true;
    }else{
        radioPayMethod.value = false;
    }

} 


const addList = async() => {

    try {
       await axios({
            url:`http://localhost:8080/operacoes`,
            method: 'POST',
            headers:{"Content-Type": "application/json"},
            data: registroModel})
    

    } catch (error) {
        console.error(error)
    }finally{
        alert('inserido com sucesso')

    }



}


const verifyCheck1 = (ids) => {
    if(ids == 1 || ids == 2)disabledButton.value = false;

}

onMounted(() => {


})


</script>
<style>

.table-container {
  display: grid;
  grid-template-columns: 65px 100px 70px;
  margin: 0%;

}

.table-container-type-payment {
  display: grid;
  grid-template-columns: 120px 140px;
  margin-left: 10%;

}
.table-container-cards {
  display: grid;
  grid-template-columns: 200px 200px 200px 200px;
  margin-bottom: 2%;
}


.table-container-type {
  display: grid;
  grid-template-columns: 200px 200px 200px;
  padding-top: 2%;
  padding-bottom: 2%;
}

.font-styles{
    color: rgb(255, 255, 255);
    font-family: sans-serif;
    font-size: large;
}


button:disabled {
    @apply bg-gray-400 hover:bg-gray-400 

}


</style>