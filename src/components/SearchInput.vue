<template>
    <div class="searchWrapper">
      <input
      id="search"
      name="search"
      :value="value"
      @input="handleChange"
      :class="{ dark: dark }"
      />
    </div>
</template>

<script>
export default {
    props: {
        value: {
            type: String,
            required: true,
        },

        dark: {
            type: Boolean,
            default: false,
        }
    },

    methods: {
        handleChange(e) {
            this.$emit('input', e.target.value);
        }
    }

}
</script>

<style lang="scss" scoped>
    .searchWrapper {
      display: flex;
      flex-direction: column;
      width: 250px;
      margin-bottom: 100px;

      input {
        height: 30px;
        border: none;
        border-bottom: 1px solid white;
        margin-top: 50px;
        color: white;
        text-align: center;
        text-transform: uppercase;
        font-size: 16px;
        font-weight: 600;
        background: none;
        transition: box-shadow .4s;

        @media (min-width: 1024px) {
            font-size: 20px;
        }

        &:focus {
            outline: none;
            box-shadow: 0 15px 25px -8px rgba(255, 255, 256, .2);
        }

        &.dark {
          color: #0b110a;
          border-bottom: 1px solid #0b110a;
        }

        &.dark:focus {
            outline: none;
            box-shadow: 0 15px 25px -8px rgba(255, 255, 256, .2);
        }
      }
    };
</style>
