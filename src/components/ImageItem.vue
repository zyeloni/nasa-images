<template>
    <div class="imageItemWrapper">
        <div class="image" :style="imageClass"></div>
    </div>
</template>

<script>
export default {
  name: 'ImageItem',
  props: {
    dataObject: {
      type: Object,
      required: true,
    },
  },

  computed: {
    imageClass() {
      return `background-image: url("${this.dataObject.links[0].href}")`;
    },
  },
};
</script>


<style lang="scss" scoped>
.image
{
    width: 250px;
    height: 250px;
    background-repeat: no-repeat;
    background-size: cover;

    &:hover{

        &:after{
            content: '';
            width: 250px;
            height: 250px;
            position: absolute;
            background-color: rgba(0, 0, 0, 0.4);
        }

    }
}

</style>
