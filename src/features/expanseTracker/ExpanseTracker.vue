<script setup>
import { ref } from "vue";

let totalBalance = ref(50000);
let incomeBalance = ref(50000);
let expanseBalance = ref(0);
let productName = ref(null);
let price = ref(null);
let isError = ref(false);
let historyItem = ref([]);
let transitionType = ref("");
let checkbalance = ref(false);


const handleSubmit = () => {


    let name = productName.value;
    let productPrice = price.value;
    if (totalBalance.value < Number(productPrice.slice(1))) {
        checkbalance.value = true;
        return;
    }

    let symbol = productPrice.charAt(0);
    let digit = productPrice.slice(1);
    // console.log(symbol);

    if (symbol === "+") {
        isError.value = false;
        totalBalance.value += Number(digit);
        productName.value = "";
        transitionType.value = "credit";
        price.value = "";
    } else if (symbol === "-") {
        isError.value = false;
        totalBalance.value -= Number(digit);
        expanseBalance.value += Number(digit);
        transitionType.value = "debit";
        productName.value = "";
        price.value = "";
    } else {
        isError.value = true;
        return;
    }

    let payload = {
        pName: name,
        pPrice: productPrice,
        type: transitionType.value
    }

    historyItem.value.push(payload)

}

</script>

<template>
    <div class="w-[25rem] bg-white p-5 rounded-lg">
        <h3 class="text-slate-800 text-2xl font-bold text-center">Expense Tracker</h3>
        <h4 class="text-slate-800 text-xl mt-2 text-center">Your Balance</h4>
        <h2 class="text-slate-900 text-5xl my-1 text-center">₹{{ totalBalance }}</h2>

        <div class="flex p-3 max-w-[18rem] my-3 mx-auto gap-10 bg-slate-50 border-2 justify-evenly">
            <div class="flex flex-col gap-2 justify-center items-center">
                <span class="text-slate-800 text-md font-bold mt-2">Income</span>
                <span class="text-2xl text-green-600 font-semibold">+₹{{ incomeBalance }}</span>
            </div>
            <div class="flex flex-col gap-2 justify-center items-center">
                <span class="text-slate-800 text-md font-bold mt-2">Expense</span>
                <span class="text-2xl text-red-600 font-semibold">-₹{{ expanseBalance }}</span>
            </div>
        </div>

        <div class="my-4">
            <h3 class="text-lg font-bold border-b-2 border-slate-200">History</h3>

            <div class="max-h-[3rem] overflow-y-auto">
                <div v-for="(item, id) in historyItem" class="flex flex-col gap-2 my-2 relative">
                    <div class="flex justify-between items-center border-2 py-1 px-3 bg-slate-50">
                        <span>{{ item.pName }}</span>
                        <span>₹{{ item.pPrice }}</span>
                    </div>

                    <div class="bg-red-900 w-2 h-9 absolute top-0 left-0"></div>
                </div>
            </div>
        </div>

        <form @submit.prevent="handleSubmit">
            <h3 class="text-lg font-bold border-b-2 my-2 border-slate-200">Add New Transaction</h3>
            <div class="flex flex-col gap-1">
                <label class="font-semibold text-md">Text</label>
                <input type="text" v-model="productName" placeholder="enter product name"
                    class="border-2 bg-slate-50 p-2 rounded-sm outline-none" name="text" id="text">
            </div>

            <div class="flex flex-col gap-1 mt-2">
                <label class="font-semibold text-md" for="amount">Amount <p>(negative-expense,positive-income)</p>
                </label>
                <input type="text" v-model="price" placeholder="enter product price"
                    class="border-2 bg-slate-50 p-2 rounded-sm outline-none" name="text" id="text">
            </div>
            <div class="flex justify-center items-center my-2">
                <button type="submit" class="bg-teal-900 text-white py-3 px-4 rounded-md">Add
                    Transaction</button>
            </div>
            <p v-if="isError" class="text-red-700 text-center font-bold">Please Add (+/-) symbol before price</p>
            <p v-if="checkbalance" class="text-red-700 text-center font-bold">Don't have enough balance</p>

        </form>
    </div>
</template>