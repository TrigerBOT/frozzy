<script setup>
import image from "~/static/images/profile.jpg";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination, Navigation, Virtual, EffectFade } from "swiper/modules";
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";
import "swiper/css/effect-fade";

const visibleUsers = ref([
  { id: 1, name: "John Doe", bio: "Software Engineer", image: image },
  { id: 2, name: "Jane Doe", bio: "Marketing Manager", image: image },
  { id: 3, name: "Lop Doe", bio: "creative Manager", image: image },
]);
const modules = [Pagination, Navigation, Virtual, EffectFade];
</script>

<template>
  <div>
  <Swiper
    :modules="modules"
    :effect="'fade'"
    :grabCursor="true"
    :slides-per-view="1"
    class="swiper"
  >
    <SwiperSlide v-for="(user, index) in visibleUsers" :key="user.id">
      <card
        :user="user"
        :virtualIndex="index"
        :is-behind="index === 1"
        loading="lazy"
      />
    </SwiperSlide>
  </Swiper>
  <Controls />
  </div>
</template>

<style scoped>
.swiper {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}
</style>
