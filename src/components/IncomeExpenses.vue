<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="money-plus " class="money plus"> +{{ props.income }}</p>
        </div>
        <div>
            <h4>Expense</h4>
            <p id="money-minus " class="money minus"> {{ props.expanse }}</p>
        </div>
        
    </div>
</template>


<script setup lang="ts">
import { defineProps } from 'vue'

const props = defineProps<{
    income:string,
    expanse: string
}>()
</script>


<style>
</style>