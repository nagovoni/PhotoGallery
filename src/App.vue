<template>
  <v-app>
    <v-main>
      <PhotoGallery />
    </v-main>
  </v-app>
</template>

<script>
import PhotoGallery from './components/PhotoGallery.vue';

export default {
  name: 'App',
  components: {
    PhotoGallery
  }
};
</script>
