<template>
  <Header/>
  <div class="container"> 
      <Balancer v-bind:total="total"/>
      <IncomeExpenses :income="income" :expanse="expanse"/>
      <TransictionList @transactionDeleted="handlerTransactionDeleted" v-bind:transactions="transactions"/>
      <Addtransiction @transactionSubmitted="handlerTransactionSubmitted"/>
  </div>
</template>

<script setup lang="ts">
import { ref,computed } from 'vue'
import { useToast } from 'vue-toastification'
import Header from './components/Header.vue'
import Balancer from './components/Balancer.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransictionList from './components/Transiction.vue'
import Addtransiction from './components/Addtransiction.vue'



const toast = useToast()
const transactions = ref([
  {id:1, text:"cash one", price: -200},
  {id:2, text:"cash two", price: 3300},
  {id:3, text:"cash tree", price: 400},
])

const total = computed( () => {
  return transactions.value.reduce( (acc, transaction) => {
    return acc + transaction.price
  },0)
})

const income = computed( () => {
  return transactions.value
  .filter( (transaction) => transaction.price > 0)
  .reduce( (acc, transaction) => {
    return acc + transaction.price
  },0).toFixed(2)
} )

const expanse = computed( () => {
  return transactions.value
  .filter( (transaction) => transaction.price < 0 )
  .reduce( (acc, transaction) => {
    return acc + transaction.price
  },0).toFixed(2)
} )

type transactionData = {
        text: string,
        price: number
    }

const generateUniqueID = () => {
  return Math.floor(Math.random() * 100000);
}
const handlerTransactionSubmitted = (data:transactionData) => {
  transactions.value.push({
    id: generateUniqueID(),
    text: data.text,
    price: data.price
  })

  toast.success('add new transaction')
}

const handlerTransactionDeleted = (id:number) => {
  transactions.value = transactions.value.filter( (transaction) => transaction.id !== id )

  toast.success('success delete transaction')
}

</script>

<style>
</style>