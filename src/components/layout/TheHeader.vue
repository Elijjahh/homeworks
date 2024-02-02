<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      searchText: '',
      timer: null as null | number
    };
  },
  watch: {
    searchText(): void {
      if (this.timer) {
        clearTimeout(this.timer);
      }

      this.timer = setTimeout(() => {
        this.updateSearchResults();
      }, 300);
    }
  },
  methods: {
    updateSearchResults(): void {
      this.$emit('search-change', this.searchText.toLowerCase());
    }
  }
});
</script>

<template>
  <header class="header">
    <div class="container flex justify-between items-center py-4">
      <div class="header__logo cursor-pointer">Vue Store</div>
      <div class="flex items-center gap-4">
        <a href="#order" class="header__link">Order</a>
        <a href="#add-product" class="header__link">Add product</a>
        <form @submit.prevent>
          <input
            type="text"
            class="header__search"
            placeholder="search by name/price"
            v-model="searchText"
          />
        </form>
      </div>
    </div>
  </header>
</template>

<style scoped lang="scss">
.header {
  &__logo {
    color: #67c4a7;
    font-size: 30px;
    font-weight: 500;
  }

  &__link {
    color: #494949;
    font-size: 18px;
    font-weight: 400;
    transition: all 0.3s;

    &:hover,
    &:focus {
      color: #67c4a7;
    }
  }

  &__search {
    border-radius: 6px;
    border: 1px solid rgba(109, 109, 109, 0.7);
    padding: 7px 15px 7px 15px;

    color: #7d7d7d;
    font-size: 12px;
    font-weight: 400;
    transition: all 0.3s;

    &:hover,
    &:focus {
      border-color: #67c4a7;
      outline: none;
    }
  }
}
</style>
