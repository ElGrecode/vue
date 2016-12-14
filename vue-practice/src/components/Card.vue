<template>
  <div id="card">
    <header>{{title}}</header>
    <div>
      <input id="itemForm" />
      <button>Add Dinosaur</button>
    </div>
    <ul>
      <li v-for="item in items">
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'card',
  data() {
    return {
      title: 'Dinosaurs',
      items: [
        { text: 'Velociraptor' },
        { text: 'Triceratops' },
        { text: 'Stegosaurus' },
      ],
    };
  },
};
</script>
