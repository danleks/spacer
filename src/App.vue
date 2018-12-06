<template>
  <div id="app">
    <div :class="[{flexStart: step === 1}, 'wrapper']">
      <transition name="logo">
        <img class="logo" v-if="step === 1" src="./assets/logo.png" alt="logo">
      </transition>
      <transition name="fade">
        <HeroImage v-if="step === 0"/>
      </transition>
      <Claim v-if="step === 0"/>
      <SearchInput v-model="searchQuery" @input="handleInput" :dark = "step === 1"/>
      <div class="results" v-if="result && loading === true && step === 1">
          <Item @click.native="handleModelOpen(item)" v-for="item in result" :item="item" :key="item.data[0].nasa_id"/>
      </div>
      <Modal v-if="modalOpen" :item="modalItem" @modalClose="modalOpen = false"/>
  </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';


const API = 'https://images-api.nasa.gov/search?q=';

export default {
  name: 'Search',
  data() {
    return {
      modalOpen: false,
      modalItem: null,
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
    Item,
    Modal,
  },

  methods: {
    handleModelOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
      console.log(item);
    },
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}${this.searchQuery}&media_type=image`)
        .then((response) => {
          console.log(response.data.collection.items);
          this.result = response.data.collection.items;
          this.step = 1;
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
    position: relative;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;
    width: 100%;
    height: 100vh;
    color: #fff;

    .logo {
      position: absolute;
      top: 20px;
    }

    &.flexStart {
      justify-content: flex-start;
    }
  };

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.logo-enter-active, .logo-leave-active {
  transition: margin-top .5s;
}

.logo-enter, .logo-leave-to {
  margin-top: -50px;
}

.results {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;

  @media (min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
</style>
