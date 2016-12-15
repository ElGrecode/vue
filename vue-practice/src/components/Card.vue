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
        <h4>{{ dino.text | capitalize }}</h4>
        <button v-on:click="dino.quantity -= 1">-</button>
          {{dino.quantity}}
        <button v-on:click="dino.quantity += 1">+</button>
        <button v-on:click="deleteItem(index)">Make Extinct</button>
        <hr />
      </li>

    </ul>
    <ul>
      <li>Total Dinosaurs: {{ totalDinos }} <span>Updated: {{ dinosUpdated }}</span></li>
      <li>Total Species: {{ totalSpecies }} <span>Updated: {{ speciesUpdated }}</span></li>
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
      totalDinos: 0,
      totalSpecies: 0,
      dinosUpdated: 0,
      speciesUpdated: 0,
      dinos: [
        {
          text: 'velociraptor',
          quantity: 5,
          weight: '15kg',
        },
        {
          text: 'triceratops',
          quantity: 3,
          weight: '6,000kg',
        },
        {
          text: 'stegosaurus',
          quantity: 6,
          weight: '2,500kg',
        },
      ],
      addItem: (e) => {
        e.preventDefault();
        const input = document.getElementById('itemForm');
        if (input.value !== '') {
          this.dinos.push({
            text: input.value,
          });
          input.value = '';
        }
      },
      deleteItem: (index) => {
        this.dinos.splice(index, 1);
      },
    };
  },
  /* eslint-disable no-param-reassign */
  computed: {
    totalDinos: (card) => {
      // NOTE: Although this works, it is a heavy MUTABLE ANTI-PATTERN
      // THERE SHOULD BE NO SIDE EFFECTS WITHIN A COMPUTED PROPERTY
      card.dinosUpdated += 1;
      return card.dinos.reduce((p, c) => p + c.quantity, 0);
    },
    totalSpecies: (card) => {
      // NOTE: Although this works, it is a heavy MUTABLE ANTI-PATTERN
      // THERE SHOULD BE NO SIDE EFFECTS WITHIN A COMPUTED PROPERTY
      card.speciesUpdated += 1;
      return card.dinos.length;
    },
  },
};
</script>
