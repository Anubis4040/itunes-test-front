<template>
  <div id="main-content" class="d-flex flex-column align-center justify-center">
    <h1 class="mb-7">Buscador de musica</h1>
    <div class="d-flex align-center justify-center find-input mb-6">
      <v-text-field
        class="mr-5"
        label="Artisa o Banda Musical"
        placeholder="Ingresa un nombre"
        filled
        background-color="white"
        hide-details=true
        v-model="search"
      ></v-text-field>
      <v-btn @click="getSongs">
        Buscar
        <v-icon >mdi-magnify</v-icon>
      </v-btn>
    </div>
    <v-progress-circular
      v-if="loading"
      indeterminate
      color="white"
    ></v-progress-circular>
    <div v-else-if="!songs?.results || songs?.results < 1" class="white--text">
      No hay resultados para mostrar
    </div>
    <v-simple-table id="songsTable" class="mb-10 elevation-10" v-else >
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              Nombre cancíon
            </th>
            <th class="text-left">
              Nombre Almbum
            </th>
            <th class="text-left">
              Url
            </th>
            <th class="text-left">
              Precio
            </th>
            <th class="text-left">
              Fecha de lanzamiento
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(item, index) in songs.results"
            :key="index"
          >
            <td>{{ item.trackName }}</td>
            <td>{{ item.collectionName }}</td>
            <td> <a :href="item.previewUrl"> Preview </a> </td>
            <td>{{ item.trackPrice }}</td>
            <td>{{ item.releaseDate | moment("DD-MM-YYYY") }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "Home-component",
  components: {},
  mounted() {
    this.getSongs()
  },
  data: () => ({
    songs: '',
    search: 'Shakira',
    loading: true
  }),
  methods: {
    getSongs:  function () {
      this.loading = true

      const params = {
        artistName: this.search
      }

      axios.get(
        `${process.env.VUE_APP_ITUNES_API_URL}/songs`,
        {
          params
        }
      )
      .then((response) => {
        this.songs = response.data
        this.loading = false
      })
    }
  }
};
</script>

<style scoped>
#main-content {
  margin-top: 90px;
}
#songsTable {
  max-width: 80%;
}
.find-input {
  width: 45%;
}
.c-shadow-1{
  box-shadow: 5px 5px;
}
</style>
