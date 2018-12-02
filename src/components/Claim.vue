<template>
    <div class="claimWrapper">
        <h1 class="claimWrapper__heading">Spacer</h1>
        <p class="claimWrapper__content">
            Begin your journey through our amazing galaxy, and discover places you never even heard of.
        </p>
        <p class="claimWrapper__content">
            Type anything space-related to start.
        </p>
    </div>
</template>

<script>
export default {
    name: 'Claim'
}
</script>

<style lang="scss" scoped>
    .claimWrapper {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;

        &__heading {
            margin-bottom: 25px;
            font-size: 50px;
            text-transform: uppercase;
        }

        &__content {
            &:not(:last-child) {
                margin-bottom: 15px;
            }
        }


    }
</style>

