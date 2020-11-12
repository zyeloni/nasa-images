<template>
  <div class="wrapper">
    <transition name="fade">
      <Hero v-if="step === 0" class="hero" />
    </transition>
    <SearchText ref="box" :hasNoResult="hasNoResult" v-if="step === 0" @input="handleInput" :SearchValue.sync="searchValue" />
    <transition-group name="fade">
    <div class="ImageWrapper" key="1" v-if="results.length != 0 && results">
        <div class="full">
          <span @click="SearchAgain">X</span>
        </div>
        <div class="ImageItem" v-for="(item,index) in results" :key="index">
          <ImageItem :dataObject="item"  />
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>

import debounce from 'lodash/debounce';
import axios from 'axios';
import SearchText from '../components/SearchText.vue';
import Hero from '../components/Hero.vue';
import ImageItem from '../components/ImageItem.vue';

// lib


// CONST DATA
const API_BASE = 'https://images-api.nasa.gov/search';


export default {
  name: 'home',
  components: {
    SearchText,
    Hero,
    ImageItem,
  },
  data() {
    return {
      searchValue: '',
      results: [],
      step: 0,
      hasNoResult: false,
    };
  },

  methods: {
    handleInput: debounce(function () {
      const vm = this;
      this.hasNoResult = false;
      this.loading = true;
      if (vm.searchValue == '') return;

      axios.get(`${API_BASE}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          if (response.data.collection.items.length != 0) {
            vm.results = response.data.collection.items;
            vm.step = 1;
          } else {
            vm.hasNoResult = true;
          }
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),

    SearchAgain() {
      this.results = [],
      this.searchValue = '';
      this.step = 0;
      this.hasNoResult = false;
    },
  },

};
</script>

<style lang="scss" scoped>

.ImageWrapper
{
  display: grid;
  grid-template-columns: 250px 250px 250px;
  grid-gap: 5px;

  @media (min-width: 1250px) {
    grid-template-columns: 250px 250px 250px 250px;
  }

  @media (max-width: 1000px) {
    grid-template-columns: 250px 250px;
  }

  @media (max-width: 650px) {
    grid-template-columns: 250px;
  }
}

.full
{
  position: fixed;
  top:10px;
  right: 30px;
  font-weight: bold;
  font-size: 30px;
  padding: 5px;

  span{
    cursor: pointer;
  }
}

.wrapper
{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    widows: 100%;
    padding: 0;
    margin: 0;
}

.hero{
  position: absolute;
  z-index: -1;
}

.fade-enter-active {
  transition: opacity .3s;
}


.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
