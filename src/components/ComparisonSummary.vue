<script setup>
import { computed, defineProps } from "vue";

const props = defineProps({
  itemA: {
    required: true,
    type: Object,
  },
  itemB: {
    required: true,
    type: Object,
  },
});

const diff = computed(() => {
  return Math.floor(
    props.itemA.price > props.itemB.price
      ? props.itemA.price / props.itemB.price
      : props.itemB.price / props.itemA.price
  );
});

const itemX = computed(() => props.itemA.price > props.itemB.price ? props.itemB : props.itemA);
const itemY = computed(() => itemX === props.itemA ? props.itemB : props.itemA);
</script>
<template>
  <p class="mx-5 text-center">
    <div v-if="props.itemA === undefined || props.itemB === undefined">
      Please select 2 items to compare.
      </div>
      <div v-else>
        <div v-if="(props.itemA.id === props.itemB.id)">
          <em>These are the same items.</em>
        </div>
        <div v-else>
          You can get <strong>{{diff}}</strong> <em>{{itemX.title}}</em> for about the same price as
      a single <em>{{itemY.title}}</em>
        </div>
      </div>
  </p>
</template>
