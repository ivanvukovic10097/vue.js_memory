<template>
  <li class="card" :style="{ order: Math.floor(Math.random() * 100) + 1 }">
  <img :src="`https://picsum.photos/id/${cardID * 25}/400/400`" alt >
  </li>
</template>

<style>
.card {
  padding:0;
  margin:0;
  background-size:100% 100%;
  background-color:#CC2039;
  cursor: pointer;
  overflow: hidden;
  transition: transform 1s;
}

.card:hover {
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25);
}

.card img {
  padding:0;
  transition: transform 0.8s;
  transform-style: preserve-3d;
  object-fit:cover;
  width: 100%;
  height: 100%;
  opacity: 0;
}

.card.is-Clicked {
  pointer-events: none;
  transform: translateX(0%) rotateY(-180deg);
  box-shadow: 1px 1px 30px rgba(0, 0, 0, 0.2);
}

.card.is-Clicked:nth-child(odd) {
  pointer-events: none;
  transform: translateX(0%) rotateY(-180deg);
  box-shadow: 1px 1px 30px rgba(0, 0, 0, 0.2);
}

.card.is-Clicked img {
  opacity: 1;
  transform:translateX(0%);
}

.card.is-Revealed {
  transform: none !important;
  box-shadow: none;
  pointer-events: none;
}

.card.is-Revealed img {
  opacity: 1;
}
</style>


<script>
export default {
  props: ["n"],
  computed: {
    cardID() {
      if (this.n % 2 === 0) {
        return this.n - 1;
      } else {
        return this.n;
      }
    }
  }
};
</script>