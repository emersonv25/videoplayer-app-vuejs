<template>
  <v-container>
    <v-row v-if="videos.length > 0"> 
      <v-col cols="12"><v-btn outlined color="primary" to="upload"> <v-icon>mdi-video-plus</v-icon> Enviar</v-btn></v-col>
      <v-col cols="12" lg="3" md="4" v-for="i in videos" :key="i.id">
        <v-card class="mx-auto rounded-0" max-width="300" flat :to="'/play/' + i.id">
          <v-img
            :src="i.thumb"
             :aspect-ratio="16/9"
          ></v-img>

            <v-card-title style="padding: 5px" class="pb-0"> {{i.titulo}} </v-card-title>
            <v-card-text style="padding: 5px; padding-top: 0px">
              <div style="color: #757575">{{i.autor.nomeAutor}}</div>
              <div>{{i.visualizacoes ? i.visualizacoes : 0}} visualizações</div>
            </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row v-else>
      <v-col cols="12"><v-btn outlined color="primary" to="upload"> <v-icon>mdi-video-plus</v-icon> Enviar</v-btn></v-col>
      <v-col cols="12">
          <div>Nenhum vídeo encontrado</div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  data() {
    return {
      loading: false,
    };
  },
  computed: {
    ...mapGetters(["usuario"]),
    ...mapGetters(["videos"])
  },
  methods:{
    async getVideos(){
      this.loading = true
      await this.$store.dispatch('getVideoUser', this.usuario.id)
      this.loading = false
    }
  },
  async beforeMount(){
    await this.$store.dispatch('getVideoUser', this.usuario.id)
  }
};
</script>