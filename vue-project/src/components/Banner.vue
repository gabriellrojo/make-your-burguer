<template>
    <div class="banner">
        <h1>Make Your Burguer</h1>
    </div>
</template>

<script>
export default {
    name: "Banner"
}
</script>

<style>
    .banner{
        background-image: url("../public/img/burger.jpeg");
        background-size: cover;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        height: 25vh;
        background-position: 0 -450px;
    }

    .banner h1{
        color: rgb(226, 210, 65);
        margin-left: 50px;
    }
</style>