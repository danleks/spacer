<template>
  <div id="app">
    <div class="wrapper">
      <HeroImage v-if="step === 0"/>
      <Claim v-if="step === 0"/>
      <SearchInput v-model="searchQuery" @input="handleInput" :dark = "step === 1"/>
  </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';


const API = 'https://images-api.nasa.gov/search?q=';

export default {
  name: 'Search',
  data() {
    return {
      searchQuery: '',
      result: [],
      loading: false,
      step: 0
    };
  },

  components: {
    Claim,
    SearchInput,
    HeroImage,
  },

  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      axios.get(`${API}${this.searchQuery}&media_type=image`)
        .then((response) => {
          console.log(response.data.collection.items);
          this.result = response.data.collection.items;
        })

        .catch((error) => {
          console.log(error);
        });
    }, 800),
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  html {
    box-sizing: border-box;
  }
  *, *:before, *:after {
    box-sizing: inherit;

  }

  body {
    font-family: 'Montserrat', sans-serif;
    padding: 0;
    margin: 0;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

  }

  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;
    width: 100%;
    height: 100vh;
    color: #fff;

  };
</style>
