<!-- kanban board component. 
  holds list of implemented cards and the drop zone functionality
  also implements a custom button for adding cards to the first list
  made with the help of the following tutorial: https://www.youtube.com/watch?v=-kZLD40d-tI
  -->
<template>
  <CustomButton text="Add Item" @click="addItemToList" />
  <div class="drop-zones-container">
    <DropZone
      v-for="listId in [1, 2, 3]"
      :key="'dropzone-' + listId"
      :list-id="listId"
      @item-dropped="onDrop"
      class="drop-zone"
    >
      <Card
        v-for="item in getList(listId)"
        :key="item.id"
        :item="item"
        @drag-started="startDrag"
        @update-item="updateItem"
        @delete-item="deleteItem"
      />
    </DropZone>
  </div>
</template>

<script>
import { ref } from 'vue';
import CustomButton from './CustomButton.vue';
import DropZone from './DropZone.vue';
import Card from './DraggableCard.vue';

export default {
  components: {
    CustomButton,
    DropZone,
    Card,
  },
  setup() {
    const items = ref([
      //existing items
    ]);

    //returns list of given index
    const getList = (listId) => {
      return items.value.filter(item => item.list === listId);
    };

    //created new card item for list 1. note it auto updates the template html through getList
    const addNewCardToList = () => {
      const newItemId = items.value.length > 0 ? Math.max(...items.value.map(item => item.id)) + 1 : 1;
      items.value.push({
        id: newItemId,
        title: 'Title',
        description: 'Description',
        list: 1,
      });
    };

    //on drag emition, we save the item id in the DTO
    const startDrag = (event, itemId) => {
      event.dataTransfer.setData('itemID', itemId.toString());
    };

    //on drop emition, we get the id of the last dragged item, then 
    const onDrop = (event, listId) => {
      const itemID = event.dataTransfer.getData('itemID');
      const item = items.value.find(item => item.id.toString() === itemID);
      if (item) {
        item.list = listId;
      }
    };

    //Updates an existing item's details with new data from updatedItem
    const updateItem = (updatedItem) => {
      const index = items.value.findIndex(item => item.id === updatedItem.id);
      if (index !== -1) {
        items.value[index] = { ...updatedItem };
      }
    };

    //deletes card by id.
    const deleteItem = (itemId) => {
      items.value = items.value.filter(item => item.id !== itemId);
    };

    return {
      getList,
      addItemToList: addNewCardToList,
      startDrag,
      onDrop,
      updateItem,
      deleteItem,
    };
  },
};
</script>

<style>
.drop-zones-container {
  display: flex;
  justify-content: center;
  gap: 20px;
}

</style>
