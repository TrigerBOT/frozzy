<script>
import Card from "./Card.vue";
import image from "~/static/images/profile.jpg";

export default {
  setup() {
    const visibleUsers = ref([
      { id: 1, name: "John Doe", bio: "Software Engineer", image: image },
      { id: 2, name: "Jane Doe", bio: "Marketing Manager", image: image },
    ]);

    return {
      visibleUsers,
    };
  },
};
</script>

<template>
  <div class="swiper">
    <card
      v-for="(user, index) in visibleUsers"
      :key="user.id"
      :user="user"
      :is-behind="index === 1"
      ?
    ></card>
  </div>
</template>

<style scoped>
.swiper {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
