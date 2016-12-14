<template>
  <div id="card">
    <header>{{title}}</header>
    <div>
      <form v-on:submit="addItem">
        <input id="itemForm"/>
        <button type="submit">Add Dinosaur</button>
      </form>
    </div>
    <ul>
      <li v-for="(item, index) in items">
        <button v-on:click="deleteItem(index)">x</button>
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>

<script>
/* global document */
export default {
  name: 'card',
    // DOM Mutation
  data() {
    return {
      title: 'Dinosaurs',
      items: [
        { text: 'Velociraptor' },
        { text: 'Triceratops' },
        { text: 'Stegosaurus' },
      ],
      addItem: (e) => {
        e.preventDefault();
        const input = document.getElementById('itemForm');
        if (input.value !== '') {
          this.items.push({
            text: input.value,
          });
          input.value = '';
        }
      },
      deleteItem: (index) => {
        this.items.splice(index, 1);
      },
    };
  },
};
</script>
