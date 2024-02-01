<template>
  <div class="gallery">
    <div v-for="(item, ind) of items" :key="ind" class="gallery__item">
      <div class="gallery__item--img-wrapper">
        <img :src="item.url" class="gallery__item--img">
      </div>
      <button @click="changeFavourites(item)" class="gallery__item--fav">
        <svg class="gallery__item--fav__img" :class="{ active: (item.fav || false )}"></svg>
      </button>
    </div>
  </div>
</template>

<script>
export default {
    props: ['items', 'callback'],

    methods: {
        changeFavourites(item) {
            this.callback(item);
        }
    }
}
</script>

<style scoped>
  .gallery {
    display: flex;
    flex-wrap: wrap;
    padding: 48px 62px;
    gap: 12px;
  }

  .gallery__item {
    height: 256px;
    width: 256px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }

  .gallery__item:hover {
    box-shadow: 0px 9px 18px 0px #0000002E;
    box-shadow: 0px 6px 5px 0px #0000003D;
  }

  .gallery__item:hover .gallery__item--fav {
    opacity: 1;
  }

  .gallery__item--img-wrapper {
    height: 225px;
    width: 225px;
    overflow: hidden;
  }

  .gallery__item--img {
    height: 100%;
    width: 100%;
    object-fit: cover
  }

  .gallery__item--fav {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    top: 189px;
    left: 193px;
    height: 48px;
    width: 48px;
    opacity: 0;
    background: none;
    border: none;
    cursor: pointer;
  }

  .gallery__item--fav__img {
    width: 100%;
    height: 100%;
    background: url('./static/assets/icons/fav.svg');
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
  }

  .gallery__item--fav__img.active {
    background: url('./static/assets/icons/fav-active.svg');
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
  }


  .gallery__item--fav:active .gallery__item--fav__img, 
  .gallery__item--fav:hover .gallery__item--fav__img {
    background: url('./static/assets/icons/fav-active.svg');
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
  }

</style>
