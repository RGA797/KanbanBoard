<!-- customizable button. can have any given logic on click.-->
<template>
    <button class ="CustomButton" @click="hanleClick">{{text}}</button>
</template>

<script>

export default {
  props: {
    text: String,
  },
  methods: {
    handleClick() {
      this.$emit('click');
    }
  }
};
</script>

<style scoped>
.CustomButton {
  background-color: var(--button-color);
  color: var(--button-text-color);
  border: none;
  padding: 10px 15px;
  border-radius: 20px; 
  text-transform: uppercase; 
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s; 
}

</style>