<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input
      id="search"
      name="search"
      v-model="searchQuery"
      @input="handleInput"/>
    </div>
    <div class="result">
      <ul>
        <li v-for="item in result" :key="item.data[0].nasa_id">
          <p>{{ item.data[0].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search?q=';

export default {
  name: 'Search',
  data() {
    return {
      searchQuery: '',
      result: [],
    };
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

<style lang="scss" scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0;
    margin: 0;
    width: 100%;
    .search {
      display: flex;
      flex-direction: column;
      width: 250px;
      label {
        font-family: sans-serif;
      };
      input {
        height: 30px;
        border: none;
        border-bottom: 1px solid black;
      }
    };
    .result {
      width: 200px;
    };
  };
</style>
