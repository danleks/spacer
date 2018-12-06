<template>
    <div class="item" :style="style"></div>
</template>

<script>
export default {
    name: 'Item',
    props: {
        item: {
            type: Object,
            required: true,
        }
    },

    data() {
        return {
            img: this.item.links[0].href,
            title: this.item.data[0].title,
        }
    },

    computed: {
        style() {
            return `background-image: url("${this.img}")`;
        }
    }
}
</script>

<style lang="scss" scoped>
    .item {
        width: 35vw;
        height: 115px;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: 50%;

        @media (min-width: 768px) {
            width: 22vw;
            height: 150px;
        }

         @media (min-width: 1024px) {
            width: 28vw;
            height: 250px;
        }
    }


</style>
