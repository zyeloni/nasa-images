<template>
    <div class="wrapper">
        <div class="image"></div>
    </div>
</template>


<script>
export default {
  name: 'Hero',
};
</script>

<style lang="scss" scoped>

.wrapper
{
    width: 100%;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;;
}

.image{
    background-image: url("../assets/hero.jpg");
    width: 100%;
    height: 100vh;
    background-size: cover;
    &::before
    {
        content: "";
        background-color: rgba(0,0,0,.5);
        position: absolute;
        width: 100%;
        height: 100vh;
    }
}
</style>
