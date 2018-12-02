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
        min-height: 100%;
        z-index: -1;
        background-image: url(../assets/heroimage.jpg);
        background-repeat: none;
        background-size: cover;
        background-position: 80% 0;
    }
</style>
