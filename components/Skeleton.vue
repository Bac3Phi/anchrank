<template>
    <section>
        <div class="chip-loading">
            <img src='~assets/source.gif' width="300">
            <p>Loading...</p>
        </div>
        <!-- <b-skeleton width="87%" :animated="animated"></b-skeleton>
        <b-skeleton width="40%" :animated="animated"></b-skeleton>
        <b-skeleton width="80%" :animated="animated"></b-skeleton>
        <b-skeleton width="30%" :animated="animated"></b-skeleton>
        <b-skeleton width="50%" :animated="animated"></b-skeleton>
        <b-skeleton width="90%" :animated="animated"></b-skeleton>
        <b-skeleton :animated="animated"></b-skeleton> -->

    </section>
</template>

<script>
export default {
    data() {
        return {
            animated: true
        }
    }
}
</script>
<style lang="scss">
    .chip-loading{
        width: 100%;
        margin: 0 auto;
        text-align: center;
    }
</style>