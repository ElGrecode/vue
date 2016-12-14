<template>
  <div id="card">
    <header>{{title | capitalize}}</header>
    <div>
      <form v-on:submit="addItem">
        <input id="itemForm"/>
        <button type="submit">Add Dinosaur</button>
      </form>
    </div>
    <ul>
      <li v-for="(dino, index) in dinos">
        <button v-on:click="deleteItem(index)">x</button>
        <h4>{{ dino.text | capitalize }}</h4>
        <span>The {{ dino.text | capitalize }} weighs {{ dino.weight }}.</span>
      </li>
    </ul>
  </div>
</template>

<script>
/* global document */
export default {
  name: 'card',
  filters: {
    capitalize: (w) => {
      if (!w) return '';
      const val = w.toString();
      return val.charAt(0).toUpperCase() + val.slice(1);
    },
  },
    // DOM Mutation
  data() {
    return {
      title: 'Dinosaurs',
      dinos: [
        {
          text: 'velociraptor',
          weight: '15kg',
        },
        {
          text: 'triceratops',
          weight: '6,000kg',
        },
        {
          text: 'stegosaurus',
          weight: '2,500kg',
        },
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
