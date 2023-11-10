<script setup lang="ts">
import '../assets/styles/_mixins.scss'

defineProps(['sidebars', 'activeStep'])
</script>

<template>
  <ul class="sidebar">
    <li v-for="( value, index) of sidebars" class="sidebar_list">
      <div class="no_of_steps" :class="{ active: index == activeStep }">{{ index + 1 }}</div>
      <div class="current_step">
        <p class="current_step_text">STEP {{ index + 1 }}</p>
        <p class="current_step_info">{{ value }}</p>
      </div>
    </li>
  </ul>
</template>
<style lang="scss" scoped>
@use '../assets/styles/_index.scss' as *;

.sidebar {
  border: 2px solid #000;
  padding: $s1;
  width: 250px;
  height: 100%;
  background-image: url(../assets/images/bg-sidebar-desktop.svg);
}

.sidebar_list {
  width: 100%;
  margin-bottom: $s1;
  @include custom_flex($ai: center);
}

.no_of_steps {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  border: 1px solid #000;
  margin-right: $s1;
  @include custom_flex($jc: center, $ai: center);
}

.current_step {
  &_text {
    color: $Cool_gray;
  }

  &_info {
    color: $White;

    font: {
      weight: $fw_7;
    }
  }
}

.active {
  background: {
    color: #fff;
  }

  color: #000;
}
</style>
