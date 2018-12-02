<template>
    <div class="heroImage" />
</template>

<script>
export default {
    name: 'HeroImage',
}
</script>

<style lang="scss" scoped>
    .heroImage {
        position: fixed;
        top: 0;
        width: 100%;
        min-height: 100vh;
        z-index: -1;
        background-image: url(../assets/heroimage.jpg);
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 80% 0;
    }

    .heroImage::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        height: 100vh;
        width: 100%;
        z-index: 1;
        background-color: rgba(0, 0, 0, .3);
    }
</style>
