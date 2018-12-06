<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img :src="img" :alt="title">
            </div>
            <div class="description">
                <h2 class="title">{{ title }}</h2>
                <div class="content">{{ description }}</div>
            </div>
        </div>
        <div class="close" @click="$emit('modalClose')"/>
    </div>
</template>

<script>
export default {
    name: 'Modal',

    data() {
        return {
            img: null,
            title: null,
            description: null,
        }
    },

    props: {
        item: {
            type: Object,
            required: true,
        }
    },

    mounted() {
        this.img = this.item.links[0].href;
        this.title = this.item.data[0].title;
        this.description = this.item.data[0].description.substring(0, 200);
    }
}
</script>

<style lang="scss" scoped>

.outerWrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    color: black;
    background-color: #e5e5e5;

    @media (min-width: 1024px) {
        width: 80%;
        height: 40%;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        margin: auto;
    }

    .innerWrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        height: 100%;
        padding: 50px;

        @media (min-width: 1024px) {
            flex-direction: row;
        }
    }

    .photo {
        width: 100%;
        height: auto;
        background-color: black;

        @media (min-width: 1024px) {
            width: 50%;
            margin-right: 38px;
        }

        img {
            display: block;
            width: 100%;
        }
    }

    .close {
        position: absolute;
        top: 0;
        right: 0;
        width: 20px;
        height: 20px;
        padding: 15px;
        cursor: pointer;


        &::before,
        &::after {
            content: '';
            display: block;
            position: absolute;
            top: 20px;
            right: 20px;
            width: 13px;
            height: 2px;
            background-color: black;

            @media (min-width: 768px) {
                top: 40px;
                right: 30px;
                width: 18px;

            }
        }

        &::before {
            transform: rotate(45deg);
        }

        &::after {
            transform: rotate(-45deg);
        }
    }
}

</style>
