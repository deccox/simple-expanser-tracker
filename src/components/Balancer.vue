<template>
    <h4>Your Balancer</h4>
    <h1 id="balance">${{props.total}}</h1>
</template>


<script setup lang="ts">
import { defineProps } from 'vue';

type Tot = {value:number}
const props = defineProps<{
    total: number
}>()
</script>