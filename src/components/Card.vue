<template>
  <div class="Card" :class="{ wide: isWide }">
    <video v-if="item.has_video" autoplay muted loop class="Card__Media">
      <source :src="item.videos[videoIdx]" type="video/mp4" />

      Sorry, your browser doesn't support embedded videos.
    </video>

    <img v-else :src="item.photos[photoIdx]" alt="" class="Card__Media" />
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    item: {
      type: Object,
      required: true,
    },
    idx: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      photoIdx: 0,
      videoIdx: 0,
    };
  },
  computed: {
    /**
     * Set the type of card either small or wide
     */
    isWide() {
      // Index of wide card from the design
      const cardsIdx = [5, 9, 11];

      return cardsIdx.includes(this.idx + 1);
    },
    /**
     * Check the type of media item
     */
    hasVideo() {
      return this.item.has_video;
    },
  },
};
</script>

<style scoped>
.Card {
  position: relative;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  border-radius: 8px;
}

.Card__Media {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  width: 100%;
  height: 100%;
}

img.Card__Media,
video.Card__Media {
  object-fit: cover;
  aspect-ratio: 16/9;
}

.wide {
  grid-column: span 2;
  grid-row: span 2;
}
</style>
