<template>
  <div>
    <my-input v-model="number" :scale="3"></my-input>
    App Unmasked: {{number}}
  </div>
</template>

<script>
import MyInput from './components/MyInput.vue';

export default {
  components: {
    MyInput,
  },
  data() {
    return {
      number: '12,',
    };
  },
};
</script>
