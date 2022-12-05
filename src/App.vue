<template>
  <div>
    <HeaderPage @queryChange="search" />
    <MainPage
      :data-movies="dataMovies"
      :data-tv="dataTv"
      @changePage="changePage"
    />
  </div>
</template>

<script>
import axios from 'axios';
import Vue from 'vue';
import HeaderPage from '@/components/HeaderPage.vue';
import MainPage from '@/components/MainPage.vue';

export default {
  name: 'App',
  components: {
    HeaderPage,
    MainPage,
  },
  data() {
    return {
      baseApiUrl: 'https://api.themoviedb.org/3',
      apiKey: 'eddeb9cc139fc5540af4fe0bcd294c59',
      resultsLanguage: 'it-IT',
      dataMovies: null,
      dataTv: null,
      queryString: '',
    };
  },
  methods: {
    search(queryString) {
      // chiamata axios all'url di ricerca
      // BASE_URL + END_POINT + (QUERY_STRING)
      this.queryString = queryString;

      axios.get(`${this.baseApiUrl}/search/movie`, {
        params: {
          api_key: this.apiKey,
          language: this.resultsLanguage,
          query: queryString,
        },
      })
        .then((responseAxios) => {
          this.dataMovies = responseAxios.data;
          responseAxios.data.results.forEach((objMovie) => {
            axios.get(`${this.baseApiUrl}/movie/${objMovie.id}/credits`, {
              params: {
                api_key: this.apiKey,
              },
            })
              .then((axiosResponse) => {
                const movie = objMovie;
                Vue.set(movie, 'cast', axiosResponse.data.cast.slice(0, 5).map((objActor) => objActor.name));
              });
          });
        });

      axios.get(`${this.baseApiUrl}/search/tv`, {
        params: {
          api_key: this.apiKey,
          language: this.resultsLanguage,
          query: queryString,
        },
      })
        .then((responseAxios) => {
          this.dataTv = responseAxios.data;
        });
    },
    changePage(info) {
      switch (info.type) {
        case 'movie':
          axios.get(`${this.baseApiUrl}/search/movie`, {
            params: {
              api_key: this.apiKey,
              language: this.resultsLanguage,
              query: this.queryString,
              page: info.page,
            },
          })
            .then((responseAxios) => {
              this.dataMovies = responseAxios.data;
            });
          break;

        case 'tv':
          axios.get(`${this.baseApiUrl}/search/tv`, {
            params: {
              api_key: this.apiKey,
              language: this.resultsLanguage,
              query: this.queryString,
              page: info.page,
            },
          })
            .then((responseAxios) => {
              this.dataTv = responseAxios.data;
            });
          break;

        default:
          break;
      }
    },
  },
};
</script>

<style lang="scss">
@import '@/assets/scss/reset';

</style>
