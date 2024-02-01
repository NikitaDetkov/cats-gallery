<template>
  <Gallery :items="items" :callback="callback"/>
</template>

<script>
const API_KEY = 'live_udU1eUrPrEENMS9V0sc1rYuBMUMerwoxuefdDkhI901JzCaqfjXswKJX3aXBe3Bi';
const url = `https://api.thecatapi.com/v1/images/search?limit=20&api_key=${API_KEY}`;

localStorage.removeItem('cats');

function handler() {}

export default {
    name: 'Index',
    layout: 'main_layout',

    data: () => ({
      items: [],
      isLoading: false
    }),

    async mounted() {
      this.items = JSON.parse(localStorage.getItem('cats'));
      if (!this.items?.length) {
        this.items = await this.getCats();
        localStorage.setItem('cats', JSON.stringify(this.items));
      }
      window.removeEventListener('scroll', handler);
      window.addEventListener('scroll', this.throttle(this.checkPosition, 250));

      let favourites = JSON.parse(localStorage.getItem('favourites')) || [];

      let favouritesObj = {}; 
      favourites?.forEach(elem => favouritesObj[elem?.id] = elem);

      this.items.forEach(elem => {
        if (!favouritesObj?.[elem?.id]) {
          elem.fav = false;
        }
      })
    },

    methods: {
      async getCats() { 
        try {
          const res = await fetch(url);
          const cats = await res.json();
          return cats;
        } catch {
          console.log('Error');
        }
        return null;
      },

      callback(item) {
        let favourites = JSON.parse(localStorage.getItem('favourites')) || [];
        const indexElem = favourites.findIndex(elem => elem.id === item.id);

        if (indexElem === -1) {
          favourites.push(item);
          item.fav = true;
        } else {
          item.fav = false;
          favourites = [...favourites.slice(0, indexElem), ...favourites.slice(indexElem + 1, favourites.length)];
        }

        this.items = [...this.items];
        localStorage.setItem('cats', JSON.stringify(this.items));
        localStorage.setItem('favourites', JSON.stringify(favourites));
      },

      async checkPosition() {
        const height = document.body.offsetHeight
        const screenHeight = window.innerHeight
        const scrolled = window.scrollY
        const threshold = height - screenHeight / 4
        const position = scrolled + screenHeight

        if (position >= threshold) {
          if (!this.isLoading) {
            this.isLoading = true;
            const newItems = await this.getCats();
            this.isLoading = false;
            this.items = [...this.items, ...newItems];
            localStorage.setItem('cats', JSON.stringify(this.items));
          }
        }
      },

      throttle(callee, timeout) {
        let timer = null

        return function perform(...args) {
          if (timer) return

          timer = setTimeout(() => {
            callee(...args)

            clearTimeout(timer)
            timer = null
          }, timeout)
        }
      }
    }
}

</script>
