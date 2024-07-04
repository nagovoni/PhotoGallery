<template>
  <v-app>
    <v-main>
      <v-container fluid>
       
        <v-row>
          <v-col>
            <v-sheet class="ml-0 mt-n12 py-6 pa-sm-6 pb-md-8 radius-card v-card v-card--flat theme--light white" style="height: 555px; max-width: 1264px;">
              <v-row class="pt-4">
                <v-col cols="12" md="6" class="d-flex ma-0 pa-2">
                  <v-img
                    v-if="photos.length > 0"
                    :src="photos[0].url"
                    class="v-responsive mx-auto mr-md-6 mr-lg-3 theme--light"
                    cover
                    style="height: 290px; border-radius: 20px 40px 40px 1px !important;">
                    <div class="v-responsive__content"></div>
                  </v-img>
                </v-col>
                <v-col cols="12" md="6" class="d-flex ma-0 pa-2">
                  <v-img
                    v-for="(photo, index) in photos.slice(1, 3)"
                    :key="index"
                    :src="photo.url"
                    class="v-responsive mr-lg-3 radius-card theme--light"
                    cover
                    style="height: 290px; border-radius: 20px 40px 40px 1px !important;">
                  </v-img>
                </v-col>
              </v-row>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>

      <v-container fluid>
        <v-row>
          <v-col v-for="(room, i) in rooms" :key="i" cols="3" xs="6" sm="4">
            <v-img :src="room.url" :alt="`Imagem do Quarto ${i + 1}`" class="image-container" />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      photos: [],
      rooms: []
    };
  },
  created() {
    this.loadPhotos();
    this.loadRooms();
  },
  methods: {
    async loadPhotos() {
      const apiUrl = 'https://api.360suites.com.br/room-api/233789';
      try {
        const response = await axios.get(apiUrl);
        this.photos = response.data.property.propertyImages.slice(0, 3); // Pegando as três primeiras fotos
      } catch (error) {
        console.error('Erro ao carregar fotos:', error);
      }
    },
    handleImageError(event) {
      console.error('Erro ao carregar imagem:', event.target.src);
      // Opcionalmente lidar com erros de imagem (ex.: exibir um ícone de imagem quebrada)
    },
    async loadRooms() {
      const apiUrl = 'https://api.360suites.com.br/room-api/233789';
      try {
        const response = await axios.get(apiUrl);
        this.rooms = response.data.images; // Substitua "your_image_property_name" pelo nome correto da propriedade
      } catch (error) {
        console.error('Erro ao carregar fotos:', error);
      }
    },
  }
};
</script>

<style scoped>
.v-img {
  max-height: 300px;
}
</style>
