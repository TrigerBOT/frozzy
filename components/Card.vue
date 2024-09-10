<script setup>
defineProps({
  user: {
    image: String,
    title: String,
    bio: String,
  },
});
</script>

<template>
  <div class="card-container">
    <div class="card">
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
// ВЫНЕСТИ В ПЛАГИНЫ
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
  opacity: 0.7;
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
    -webkit-backdrop-filter: blur(
      15px
    ); /* for Safari and Chrome */ /* rounded corners */ /* add some padding */
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
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    font-size: 18px;
    width: 100%;
    max-height: 50px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: normal;
  }
}
</style>
