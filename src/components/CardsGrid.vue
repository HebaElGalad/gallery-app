<template>
  <div class="CardsGrid">
    <Card v-for="(item, idx) in currentItems" :key="idx" :item="item" :idx="idx" @failed="reloadMedia(idx)" />
  </div>
</template>

<script>
import Card from '@/components/Card.vue';
import { getRandomNumber } from '@/utilities/helper';

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
  data() {
    return {
      counter: null,
      timer: 5, // 5 sec
      cardsLength: 15,
      currentItems: [],
      failedMediaIdx: null,
    };
  },
  computed: {
    mediaLength() {
      return this.items.length;
    },
  },
  beforeMount() {
    this.currentItems = this.items?.slice(0, this.cardsLength);
  },
  mounted() {
    this.counter = setInterval(() => {
      this.updateCards();
    }, this.timer * 1000);
  },
  beforeDestroy() {
    clearInterval(this.counter);
  },
  methods: {
    /**
     * Update media cards randomly
     */
    updateCards() {
      // get random card number from the currently displayed cards
      // or the idx of the broken media
      const cardIdx = this.failedMediaIdx !== null ? this.failedMediaIdx : getRandomNumber(this.cardsLength);

      // get random item number from the media items array
      const itemIdx = getRandomNumber(this.mediaLength);

      // find item in the media array with the created random number
      const newMediaItem = this.items.find((_, idx) => idx === itemIdx);

      const isMediaItemDispalyed = this.currentItems.find(item => item.id === newMediaItem.id);
      // make sure the media item won't be displayed twice
      if (isMediaItemDispalyed) {
        this.updateCards();
      }

      // replace the card's media with the new one
      this.currentItems.splice(cardIdx, 1, newMediaItem);
    },
    /**
     * Replace broken media card with a new one
     */
    reloadMedia(idx) {
      this.failedMediaIdx = idx;
      this.updateCards();
      this.failedMediaIdx = null;
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
