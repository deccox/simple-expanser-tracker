<template>
    <h3>Add New Transiction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text" > Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter Text...">

        </div>

        <div class="form-control">
            <label for="amount"> Amount <br/> 
                (negative - expense, positive - income)
            </label>
            <input type="text" id="amount" v-model="price" placeholder="Enter Amount...">
        </div>
        <button class="btn">Add Transiction</button>
    </form>
</template>


<script setup lang=ts>

import { ref } from 'vue'
import { useToast} from 'vue-toastification'

type transactionData = {
    text: string,
    price:number
}
const emit = defineEmits(['transactionSubmitted'])
const text = ref<string>('')
const price = ref<string>('')
const toast = useToast()
const onSubmit = () => {
    if(!text.value || !price.value){
        toast.error('both fileds')
        return
    }
    if (isNaN(parseInt(price.value))){
        toast.error('insert valid number')
        price.value = ''
        return;
    }   

    const transactionData:transactionData = {
        text: text.value,
        price: parseFloat(price.value)
    }
    emit('transactionSubmitted', transactionData)
    text.value = ''
    price.value = ''
}
</script>