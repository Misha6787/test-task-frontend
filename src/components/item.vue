<script setup>
  defineProps({
    itemName: {
      type: String,
      required: true
    }
  })


</script>

<template>
  <li class="item" v-on:click="">
    <h4 class="item__name">
      {{ itemName }}
    </h4>
  </li>
</template>

<style scoped>
  .item {
    padding: 0 8px;
    cursor: pointer;
    user-select: none;
    transition: 0.2s ease;
  }

  .item:hover {
    box-shadow: 0 0 2px 1px rgba(0, 0, 0, 0.2);
  }

  .item:active {
    box-shadow: 0 0 2px 1px rgba(0, 0, 0, 0.4);
  }
</style>