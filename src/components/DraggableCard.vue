<template>
  <div class="card" draggable="true" @dragstart="startDrag">
    <!-- note: @blur updates item on losing focus: ie- clicking away after edit-->
    <input class ="title" type="text" v-model="editableItem.title" @blur="updateItem" placeholder="Title" />
    <textarea class ="description" v-model="editableItem.description" @blur="updateItem" placeholder="Description"></textarea>
    <div class = "deleteButtonContainer">
      <CustomButton text="X" @click="deleteItem" />
    </div>
  </div>
</template>

<script>
import CustomButton from './CustomButton.vue'; 

export default {
  components: {
    CustomButton, 
  },
  props: {
    item: {
      type: Object,
      required: true,
      //for proper implementation should have:
      //id: number,
      //title: 'Title',
      //description: 'Description',
      //list: number,
    },
  },
  data() {
    return {
      editableItem: { ...this.item },
    };
  },
  methods: {
    //dragging functionality for whole card. saves itemid to DTO.
    startDrag(event) {
      event.dataTransfer.setData('itemID', this.editableItem.id.toString());
      event.dataTransfer.effectAllowed = 'move';
    },
    //update item. used on title and description edit
    updateItem() {
      this.$emit('update-item', this.editableItem);
    },
    //delete functionality. used on custom button
    deleteItem() {
      this.$emit('delete-item', this.editableItem.id);
    },
  },
};
</script>

<style scoped>
.card {
  position: relative;
  background-color: #f7d1cd; 
  color: var(--secondary-color);
  padding: 10px;
  border-radius: 8px; 
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px; 
}

.title{
  color: var(--secondary-color);
  border: 1px solid #ddd; 
  margin: 5px 0; 
  padding: 8px;
  border-radius: 4px; 
}
.description {
  color: var(--secondary-color);
  border: 1px solid #ddd; 
  margin: 5px 0; 
  padding: 8px;
  border-radius: 4px; 
}

.deleteButtonContainer {
  position: absolute; 
  top: 0; 
  right: 0; 
  padding: 5px; 
}
</style>
