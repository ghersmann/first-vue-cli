<template>
  <button :class="styling" @click="$emit('btn-clicked')"><slot /></button>
</template>

<script>
export default {
  emits: ["btn-clicked"],
  props: {
    variant: {
      type: String,
      default: "primary",
      validator(propValue) {
        return ["primary", "secondary"].includes(propValue);
      },
    },
  },
  computed: {
    styling() {
      return ["btn", `btn--${this.variant}`];
    },
  },
};
</script>

<style scoped>
.btn {
  border: 3px solid transparent;
  border-radius: 3px;
  padding: 5px;
  width: 100%;
  cursor: pointer;
}

.btn--primary {
  opacity: 1;
  border-color: var(--primary-dark);
  background-color: var(--primary);
  color: #fff;
}

.btn--primary:hover {
  opacity: 1;
  border-color: var(--primary);
  background-color: var(--primary-dark);
}

.btn--secondary {
  border-color: var(--primary);
  background-color: transparent;
  color: var(--primary);
}

.btn--secondary:hover {
  background-color: var(--primary);
  color: #fff;
}
</style>
