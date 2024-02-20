<template>
    <h3>Thêm giao dịch mới</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Tên giao dịch</label>
            <input type="text" id="text" v-model="text" placeholder="Điền giao dịch...">
        </div>
        <div class="form-control">
            <label for="amount" 
            >Số tiền <br /></label>
            <input type="number" id="amount" v-model="amount" placeholder="Điền số tiền..." />
        </div>
        <button class="btn">Thêm giao dịch</button>
    </form>
</template>

<script setup>

import { ref } from 'vue';
import {useToast} from 'vue-toastification'
import { parse } from 'vue/compiler-sfc';

const text = ref('');
const amount = ref('');

const emit = defineEmits(['transactionSubmitted'])

const toast = useToast();



const onSubmit = () => {
    if(!text.value || !amount.value) {
        toast.error('Cần điền đầy đủ thông tin')
        return
    }

    const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
    }

    emit('transactionSubmitted', transactionData)

    text.value = ''
    amount.value = ''
    }
</script>