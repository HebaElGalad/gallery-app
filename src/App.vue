<template>
  <div id="app">
    <div class="container">
      <header>
        <h1 class="AppTitle">Things to exerince</h1>
        <ActivitiesMenu @active-link="setActiveLink" />
      </header>
    </div>
  </div>
</template>

<script>
import ActivitiesMenu from './components/ActivitiesMenu.vue';

export default {
  name: 'App',
  components: {
    ActivitiesMenu,
  },
  data() {
    return {
      activeLink: '',
    };
  },
  watch: {
    activeLink(value) {
      if (!value) {
        return;
      }
      this.getData();
    },
  },
  methods: {
    setActiveLink(link) {
      this.activeLink = link;
    },
  },
};
</script>

<style scoped>
.AppTitle {
  font-size: 30px;
  text-align: left;
  text-transform: uppercase;
}

.AppTitle::after {
  content: '';
  display: block;
  width: 100px;
  height: 3px;
  background-color: var(--primary);
}
</style>
