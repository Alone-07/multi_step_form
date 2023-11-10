<script setup lang="ts">
const props = defineProps([
  'plan',
]);
const { monthly, yearly } = props.plan
const cardHandler = (e: any) => {
  let target = e.target.closest('div')
  if (!target) return ''
  const targetClassList = target.classList;

  if (monthly.enabled) {
    for (let { selected } of monthly.availablePlans) {
      selected = false
    }
    const selectedPlan = monthly.availablePlans.filter(({ title }) => targetClassList.contains(title))
    selectedPlan[0].selected = true
  } else {
    for (let { selected } of yearly.availablePlans) {
      selected = false
    }
    const selectedPlan = yearly.availablePlans.filter(({ title }) => targetClassList.contains(title))
    selectedPlan[0].selected = true
  }


}
const switcher = () => {
  monthly.enabled = !monthly.enabled;
  yearly.enabled = !yearly.enabled;
}
</script>

<template>
  <div>
    <h1 class="head">Select your plan</h1>
    <p class="text">You have the option of monthly or yearly billing.</p>
    <div class="cards" @click="cardHandler">
      <div class="card Arcade">
        <img src="../assets/images/icon-arcade.svg" alt="arcade">
        <h5>Arcade</h5>
        <div v-show="props?.plan?.monthly?.enabled">
          <p class="price">$9/mo</p>
        </div>
        <div v-show="props?.plan?.yearly?.enabled">
          <p class="price">$90/yr</p>
          <p class="free">2 months free</p>
        </div>
      </div>
      <div class="card Advanced">
        <img src="../assets/images/icon-advanced.svg" alt="advanced">
        <h5>Advanced</h5>
        <div v-show="props?.plan?.monthly?.enabled">
          <p class="price">$12/mo</p>
        </div>
        <div v-show="props?.plan?.yearly?.enabled">
          <p class="price">$120/yr</p>
          <p class="free">2 months free</p>
        </div>
      </div>
      <div class="card Pro">
        <img src="../assets/images/icon-pro.svg" alt="pro">
        <h5>Pro</h5>
        <div v-show="props?.plan?.value?.monthly?.enabled">
          <p class="price">$15/mo</p>
        </div>
        <div v-show="props?.plan?.value?.yearly?.enabled">
          <p class="price">$150/yr</p>
          <p class="free">2 months free</p>
        </div>
      </div>
    </div>
    <div class="switch_box">
      <p class="month">Monthly</p>
      <input type="checkbox" class="switch" @click="switcher">
      <p class="year">Yearly</p>
    </div>
  </div>
</template>


<style lang="scss" scoped ></style>
