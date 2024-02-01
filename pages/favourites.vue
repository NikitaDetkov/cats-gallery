<template>
  <Gallery :items="items" :callback="callback"/>
</template>

<script>
export default {
  name: 'Favourites',
  layout: 'main_layout',

  data: () => ({
    items: [],
  }),

  async mounted() {
    this.items = this.getFavouritesCats();
  },

  methods: {
    getFavouritesCats() {     
      let items = JSON.parse(localStorage.getItem('favourites')) || [];
      return items;
    },

    callback(item) {
      let favourites = JSON.parse(localStorage.getItem('favourites')) || [];
      const indexElem = favourites.findIndex(elem => elem.id === item.id);

      item.fav = false;
      favourites = [...favourites.slice(0, indexElem), ...favourites.slice(indexElem + 1, favourites.length)];

      localStorage.setItem('favourites', JSON.stringify(favourites));

      this.items = favourites;
    }
  }
}
</script>