<script>
import "../assets/style/Button.css";

export default {
  name: "Button",
  props: {
    title: String,
    category: Array,
    option: Number,
    clicked: { 
      type: Function, 
      required: true
    }
  },
}
</script>

<template>
  <button :class="[`btn btn-${option}-${category}`]" @click="clicked">
    {{ title }}
  </button>
</template>
