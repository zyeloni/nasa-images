<template>
    <div class="wrapperSearch">
        <Claim />
        <input @input="handleInput" :class="[{'noresult': hasNoResult}, 'searchInput']" v-model="searchValue" type="text">
        <div class="error">
            <span v-if="hasNoResult">No search results !</span>
        </div>
    </div>
</template>


<script>
import Claim from './Claim.vue';

export default {
  name: 'SearchText',

  components: {
    Claim,
  },

  props: {
    SearchValue: {
      type: String,
      required: true,
    },

    hasNoResult: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    searchValue: {
      get() {
        return this.SearchValue;
      },

      set(value) {
        this.$emit('update:SearchValue', value);
      },
    },
  },
  methods: {
    handleInput() {
      this.$emit('input');
    },
  },
};
</script>

<style lang="scss" scoped>

.wrapperSearch
{
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    height: 100vh;
}

.searchInput
{
    border: none;
    border-bottom: 2px solid #E6E6FA;
    width: 90%;
    text-align: center;
    font-size: 20px;
    color: #E6E6FA;
    padding: 10px 0 10px 0;
    background: none;

    &:focus
    {
        outline: none;
    }
}

.searchInput.noresult
{
    color: rgb(197, 47, 47) !important;
    border-bottom: 2px solid rgb(197, 47, 47) !important;
}

.error
{
    margin-top: 40px;
    color: rgb(235, 96, 96);
    font-weight: bold;
    height: 19px;
}

</style>
