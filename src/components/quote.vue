<template>
  <div class="quote" @click="DeleteQuote()">
    <div class="quoteContent">
      <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    DeleteQuote() {
      this.$emit("DeleteQuote", this.quoteId);
    }
  },
  props: {
    quoteId: Number
  }
};
</script>
<style scoped>
.quote {
  width: 25%;
}
.quoteContent {
  border: 1px solid #CCC;
  box-shadow: 1px 1px 1px #33333333;
  margin: 10px;
  box-sizing: border-box;
  cursor: pointer;
}
</style>
