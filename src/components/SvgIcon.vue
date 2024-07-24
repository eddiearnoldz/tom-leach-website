<!-- SvgIcon.vue -->
<script>
import { defineAsyncComponent } from 'vue';

export default {
  props: {
    name: {
      type: String,
      required: true,
    },
  },
  computed: {
    dynamicComponent() {
      return defineAsyncComponent(() => import(`../assets/icons/${this.name}.vue`));
    },
  },
};
</script>

<template>
  <component :is="dynamicComponent" />
</template>
