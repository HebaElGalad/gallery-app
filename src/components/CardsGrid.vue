<template>
  <div class="CardsGrid">
    <Card v-for="(item, idx) in currentItems" :key="idx" :item="item" :idx="idx" />
  </div>
</template>

<script>
import Card from '@/components/Card.vue';

export default {
  name: 'CardsGrid',
  components: {
    Card,
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  computed: {
    currentItems() {
      return this.items?.slice(0, 15);
    },
  },
};
</script>

<style lang="postcss" scoped>
.CardsGrid {
  display: grid;
  grid-gap: 6px;
  grid-template-columns: repeat(auto-fit, minmax(165px, 1fr));
  grid-auto-rows: 240px;
}
</style>
