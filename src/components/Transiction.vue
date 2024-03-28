<template>
    <h3>History</h3>
        <ul id="list " class="list ">
            <li 
                v-for="trans in props.transactions"
                :key="trans.id"
                :class="trans.price < 0 ? 'minus' : 'plus'"
            >
                {{ trans.text }} <span>${{trans.price}}</span>
                <button
                    @click="deleteTransaction(trans.id)" 
                    class="delete-btn"
                >X</button>
            </li>
        </ul>
</template>


<script setup lang="ts">
import { defineProps } from 'vue';

const emit = defineEmits(["transactionDeleted"])
type Transaction = {id: number, text: string, price: number}[]

const props = defineProps<{
    transactions: Transaction
}>();

const deleteTransaction = (id:number) => {
    emit('transactionDeleted', id)
}
</script>


<style>
</style>