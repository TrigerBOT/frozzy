<script setup>
import { ref } from "vue";

defineProps({
  user : {
    image: String,
    title: String,
    bio: String,
  },
  isBehind: Boolean
});

const swipeLeft = ref(false);
const swipeRight = ref(false);
const startX = ref(0);
const deltaX = ref(0);

function handleTouchStart(event) {
  startX.value = event.touches[0].clientX;
}

function handleTouchMove(event) {
  deltaX.value = event.touches[0].clientX - startX.value;
  if (deltaX.value > 50) {
    swipeRight.value = true;
  } else if (deltaX.value < -50) {
    swipeLeft.value = true;
  }
}



</script>

<template>
  <div
    class="card-container"
    :class="{ 'glass-effect_ennabled': isBehind , 'behind': isBehind }"
    @touchstart="handleTouchStart"
    @touchmove="handleTouchMove"
  >
  <div v-if="isBehind" class="card__glush" ></div>
    <div
      class="card"
      :class="{ 'swipe-left': swipeLeft, 'swipe-right': swipeRight, 'glass-effect_ennabled': isBehind   }"
    >
      <img class="card__image" :src="user.image" alt="Image" />
      <div class="card__info glass-effect">
        <h2 class="card__name">{{ user.name }}</h2>
        <p class="card__desc">{{ user.bio }}</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
// ВЫНЕСТИ В ПЛАГИНЫ
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.glass-effect {
  background: rgba(255, 255, 255, 0.3); /* translucent white background */
  backdrop-filter: blur(15px); /* blur the background */
  -webkit-backdrop-filter: blur(15px); /* for Safari and Chrome */
  border-radius: 8px; /* rounded corners */
  padding: 4px 8px; /* add some padding */
}

.glass-effect > * {
  filter: none; /* prevent the blur effect from affecting the text */
}
.glass-effect_ennabled{
  background: rgba(255, 255, 255, 0.3); /* translucent white background */
  backdrop-filter: blur(15px); /* blur the background */
  -webkit-backdrop-filter: blur(15px); /* for Safari and Chrome */ /* rounded corners *//* add some padding */
  background: inherit;
}
//

.card-container {
  z-index: 5;
  border: 1px solid red;
  position: relative;
  min-width: 300px;
  min-height: 600px;
  overflow: hidden;
  opacity: 1;
}
.card-container.behind {
  opacity: .7;
  position: absolute;
  z-index: 0; /* card behind */
  pointer-events: none; /* make it unclickable */
}
.card {
  color: #6c5ce7;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  position: relative;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transform: translateX(0);
  transition: transform 0.3s ease-in-out;

  &__glush {
    z-index: 4;
    width: 100%;
    height: 100%;
    position: absolute;
    background: rgba(255, 255, 255, 0.3); /* translucent white background */
  backdrop-filter: blur(15px); /* blur the background */
  -webkit-backdrop-filter: blur(15px); /* for Safari and Chrome */ /* rounded corners *//* add some padding */
  }

  &__image {
    z-index: 1;
    width: 100%;
    height: 100%;
    margin: 0 auto;
    background-size: cover;
    background-repeat: no-repeat;
  }

  &__info {
    z-index: 2;
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
  }

  &__name {
    font-size: 35px;
    margin-bottom: 12px;
  }

  &__desc {
    margin-bottom: 12px;
    display: -webkit-box;
    -webkit-line-clamp: 2; /* display at least 4 lines */
    -webkit-box-orient: vertical;
    font-size: 18px;
    width: 100%;
    max-height: 50px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: normal;
  }
}

.card.swipe-left {
  transform: translateX(-100%);
}

.card.swipe-right {
  transform: translateX(100%);
}
</style>
