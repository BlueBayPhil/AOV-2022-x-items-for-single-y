<script setup>
import { ref } from 'vue'
import { useItemComparison } from '../composables/itemComparison'

const selected = ref()
const props = defineProps({
  items: {
    type: Array,
    requried: true,
  },
  modelValue: {
    type: Object,
    required: false,
  },
});
const emit = defineEmits(['update:modelValue']);

function updateValue(event) {
  const theItem = props.items.filter((i) => i.id == event.target.value)[0];
  emit('update:modelValue', theItem);
}
</script>

<template>
  <select @change="updateValue" class="p-2 border-2 border-gray-dark">
    <option disabled value="" selected>Select an item</option>
    <option v-for="item in props.items" :key="item.id" :value="item.id">{{`${item.title} - £${item.price}`}}</option>
  </select>
</template>
