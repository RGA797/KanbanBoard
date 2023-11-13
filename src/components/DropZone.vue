<!-- drop zone component. emits item drop event with custom functionality.-->
<template>
    <div
      class="drop-zone"
      @drop="handleDrop"
      @dragover.prevent
      @dragenter.prevent
    >
      <slot></slot>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      listId: {
        type: Number,
        required: true,
      },
      title: String
    },
    methods: {
      handleDrop(event) {
        event.preventDefault(); 
        this.$emit('item-dropped', event, this.listId);
      },
    },
  };
  </script>

<style scoped>

.drop-zone{
  width: 33%;
    /* space inside component elements  */
  padding: 10px;
   /* space between components borders  */
  margin: 50px auto;
  background-color: #ecf0f1;
  /* min height needed to drop items into  */
  min-height: 10px;
}
</style>
  