<script setup>
import ItemSelect from "./components/ItemSelect.vue";
import ComparisonSummary from "./components/ComparisonSummary.vue";
import { reactive } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";

const data = reactive({
  isLoading: false,
  products: [],
  productA: undefined,
  productB: undefined,
});

fetch("https://dummyjson.com/products")
  .then((res) => res.json())
  .then((list) => {
    data.products = list.products;
  });
</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Select items to compare</h1>
    <div class="flex flex-col gap-5 justify-center">
      <ItemSelect :items="data.products" v-model="data.productA" />
      <ItemSelect :items="data.products" v-model="data.productB" />
    </div>
    <ComparisonSummary :item-a="data.productA" :item-b="data.productB"/>
  </div>
</template>
