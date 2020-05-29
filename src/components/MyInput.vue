<template>
  <div>
    <el-input v-model="masked"></el-input>
  </div>
</template>

<script>
import { createMask } from 'imask';

export default {
  name: 'my-input',
  props: {
    value: String,
    min: {
      type: Number,
      default: 0,
    },
    max: {
      type: Number,
      default: 99.99,
    },
    scale: {
      type: Number,
      default: 2,
    },
  },
  data: () => ({
    innerValue: 0,
    mask: null,
  }),
  computed: {
    masked: {
      get() {
        return this.innerValue.toString();
      },
      set(value) {
        const resolved = this.mask.resolve(value.toString());
        const re = new RegExp('^\\d+[,.]$');

        if (this.scale > 0 && value.toString().match(re)) {
          this.innerValue = value.toString();
        } else {
          this.innerValue = resolved;
        }

        this.$emit('input', this.mask.unmaskedValue);
      },
    },
  },
  beforeMount() {
    this.mask = createMask({
      mask: Number,
      scale: this.scale,
      radix: ',',
      mapToRadix: ['.'],
      min: this.min,
      max: this.max,
    });
    window.mask = this.mask;
  },
  mounted() {
    this.innerValue = this.value;
  },
};
</script>
