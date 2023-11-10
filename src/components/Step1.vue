<script setup lang="ts">

const props = defineProps(['name', 'email', 'phone'])
const emit = defineEmits(['update:name', 'update:email', 'update:phone'])

const inputName = {
  labelValue: 'Name',
  placeholderValue: 'Stephen King',
  type: "text",
}
const inputEmail = {
  labelValue: 'Email Address',
  placeholderValue: 'stephenking@lorem.com',
  type: "email",

}
const inputPhone = {
  labelValue: 'Phone Number',
  placeholderValue: '+1 234 567 890',
  type: "number",
}

</script>
<template >
  <div>
    <h1 class="head">Personal info</h1>
    <p class="text">Please provide your name, email address, and phone number</p>
    <form action="javascript:void(0)" class="personal_info_form">
      <!-- name -->
      <label for="name">{{ inputName.labelValue }}</label>
      <input type="text" id="name" :placeholder="inputName.placeholderValue" :value="props.name"
        @change="emit('update:name', $event.target.value)">
      <p>{{ props.name }}</p>
      <!-- email -->
      <label for="email">{{ inputEmail.labelValue }}</label>
      <input type="email" id="email" :placeholder="inputEmail.placeholderValue" :value="props.email"
        @change="emit('update:email', $event.target.value)">
      <p>{{ props.email }}</p>
      <!-- phone number -->
      <label for="phone">{{ inputPhone.labelValue }}</label>
      <input type="tel" id="phone" :placeholder="inputPhone.placeholderValue" :value="props.phone" inputmode="numeric"
        @change="emit('update:phone', $event.target.value)">
      <p>{{ props.phone }}</p>
    </form>
  </div>
</template>


<style lang="scss" scoped >
.personal_info_form>* {
  display: block;
}
</style>
