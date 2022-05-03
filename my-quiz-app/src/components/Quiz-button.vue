<template>
  <button :disabled="!disabled">
      <slot></slot>
  </button>
</template>

<script>
export default {
    props: {
        disabled: {
            type: Boolean,
            require: false,
            default: false
        }
    }
}
</script>

<style>
    button {
        padding: 10px 30px;
        margin: 10px 0;
        
        font-size: 1rem;
        font-weight: bold;
        color: #3c2a4d;
        
        border: none;
        border-radius: 7px;
        cursor: pointer;

        transition: .5s ease;
    }
</style>