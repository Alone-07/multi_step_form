<script setup lang="ts">
const props = defineProps(['addOns',])
</script>

<template>
  <div>
    <h1 class="head">Pick add-ons</h1>
    <p class="text">Add-ons help enhance your gaming experience.</p>
    <div class="checklist">
      <div class="list" v-for="( add, index) in props.addOns" :key="index" :class="{ active: add.enabled }">
        <input type="checkbox" name="list" :id="add.feature" :checked="add.enabled" @change="add.enabled = !add.enabled">
        <div class="list_Details">
          <p class="name">{{ add.feature }}</p>
          <p class="description">{{ add.description }}</p>
          <p class="price">{{ add.priceText }}</p>
        </div>
      </div>
    </div>
  </div>
</template>


<style lang="scss" scoped >
.active {
  border: 2px solid limegreen;
}
</style>
