<script setup>
  import Item from "@/components/item.vue";
  import {ref} from "vue";

  const leftBlock = ref([
        {
          "id": 1,
          "name": "Shoes 1"
        },
        {
          "id": 2,
          "name": "Shoes 2"
        },
        {
          "id": 3,
          "name": "Shoes 3"
        },
        {
          "id": 4,
          "name": "Shoes 4"
        },
        {
          "id": 5,
          "name": "T-shirt 1"
        },
        {
          "id": 6,
          "name": "T-shirt 2"
        },
        {
          "id": 7,
          "name": "T-shirt 3"
        },
        {
          "id": 8,
          "name": "T-shirt 4"
        }
      ]),
      rightBlock = ref([
        {
          "id": 11,
          "name": "Jacket 1"
        },
        {
          "id": 12,
          "name": "Jacket 2"
        },
        {
          "id": 13,
          "name": "Jacket 3"
        },
        {
          "id": 14,
          "name": "Jacket 4"
        },
        {
          "id": 15,
          "name": "Hoodie 1"
        },
        {
          "id": 16,
          "name": "Hoodie 2"
        },
        {
          "id": 17,
          "name": "Hoodie 3"
        },
        {
          "id": 18,
          "name": "Hoodie 4"
        }
      ]);

  const selectedLeftBlock = ref([]),
      selectedRightBlock = ref([]);

  const maxSelectedLeftBlock = 6,
      maxSelectedRightBlock = 1;

  const deleteItem = (arr, index) => arr.value.splice(index, 1);
  const sortedArray = (arr) => arr.value.sort((itemCurrent, itemNext) => itemCurrent.id > itemNext.id ? 1 : -1);
  const pushItem = (arr, item) => arr.value.push(item);

  const selectItemLeft = (item, index) => {
    if (selectedLeftBlock.value.length >= maxSelectedLeftBlock) return;

    pushItem(selectedLeftBlock, item);
    deleteItem(leftBlock, index);
  }
  const selectItemRight = (item, index) => {
    if (selectedRightBlock.value.length >= maxSelectedRightBlock) return;

    pushItem(selectedRightBlock, item);
    deleteItem(rightBlock, index);
  }

  const unselectItemLeft = (item, index) => {
    pushItem(leftBlock, item);
    deleteItem(selectedLeftBlock, index);
    sortedArray(leftBlock);
  }
  const unselectItemRight = (item, index) => {
    pushItem(rightBlock, item);
    deleteItem(selectedRightBlock, index);
    sortedArray(rightBlock);
  }

</script>

<template>
  <div class="page-selected">
    <section class="selected-zone">

      <fieldset class="selected-zone__many">
        <legend class="selected-zone__title">Здесь может находиться несколько эллементов</legend>
        <!-- /.selected-zone__title -->
        <ul>
          <li v-for="(item, index) in selectedLeftBlock">
            {{ item.name }}
            <span class="selected-zone__delete" v-on:click="unselectItemLeft(item, index)">✖</span>
          </li>
        </ul>

        <div class="selected-zone__counter">{{ selectedLeftBlock.length }} / {{ maxSelectedLeftBlock }}</div>
      </fieldset>
      <!-- /.selected-zone__many -->

      <fieldset class="selected-zone__one">
        <legend class="selected-zone__title">Здесь может находиться только 1 эллемент</legend>
        <!-- /.selected-zone__title -->
        <ul>
          <li v-for="(item, index) in selectedRightBlock">
            {{ item.name }}
            <span class="selected-zone__delete" v-on:click="unselectItemRight(item, index)">✖</span>
          </li>
        </ul>

        <div class="selected-zone__counter">{{ selectedRightBlock.length }} / {{ maxSelectedRightBlock }}</div>
      </fieldset>
      <!-- /.selected-zone__one -->

    </section>
    <!-- /.selected-zone -->

    <section class="items-zone">
      <fieldset class="items-zone__left">
        <ul class="items-zone__list">
          <item v-for="(item, index) in leftBlock" :key="item.id" :itemName="item.name" v-on:click="selectItemLeft(item, index)"/>
        </ul>
      </fieldset>
      <!-- /.items-zone__left -->
      <fieldset class="items-zone__right">
        <ul class="items-zone__list">
          <item v-for="(item, index) in rightBlock" :key="item.id" :itemName="item.name" v-on:click="selectItemRight(item, index)"/>
        </ul>
      </fieldset>
      <!-- /.items-zone__right -->
    </section>
    <!-- /.items-zone -->
  </div>

</template>

<style scoped>

  .page-selected {
    margin-top: 64px;
  }

  .selected-zone,
  .items-zone {
    display: flex;
    justify-content: space-between;
    padding: 0 4px;
  }

  .selected-zone {
    margin-bottom: 4px;
  }

  .selected-zone__many,
  .selected-zone__one,
  .items-zone__left,
  .items-zone__right {
    position: relative;
    width: 50%;
  }

  .selected-zone__title {
    font-size: 20px;
  }

  .selected-zone__counter {
    position: absolute;
    bottom: 8px;
    opacity: 0.5;
  }

  .selected-zone__many,
  .selected-zone__one {
    height: 240px;
  }

  .items-zone__list {
    display: flex;
    flex-wrap: wrap;
    list-style-type: none;
    padding: 0;
  }

  .selected-zone__delete {
    cursor: pointer;
    user-select: none;
  }

</style>
