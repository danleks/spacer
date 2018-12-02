<template>
    <div class="searchWrapper">
      <input
      id="search"
      name="search"
      v-model="searchQuery"
      @input="handleInput"/>
    </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
    .searchWrapper {
      display: flex;
      flex-direction: column;
      width: 250px;

      input {
        height: 30px;
        border: none;
        border-bottom: 1px solid black;
        margin-top: 50px;
        background: none;
      }
    };
</style>
