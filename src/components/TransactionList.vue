<template>
    <h3>Lịch sử</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            {{transaction.text}} <span>${{transaction.amount}}</span>
            <button @click="deleteTransasction(transaction.id)" class="delete-btn"></button>
        </li>
    </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['transactionDeleted'])

const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    },
});

const deleteTransasction = (id) => {
    emit('transactionDeleted', id)
}
</script>
