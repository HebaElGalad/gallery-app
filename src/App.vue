<template>
  <div id="app">
    <div class="container">
      <header>
        <h1 class="AppTitle">Things to exerince</h1>
        <ActivitiesMenu @active-link="setActiveLink" />
      </header>

      <main id="main">
        <Spinner v-if="isFetching" />

        <section v-else>
          <p v-if="error" class="Error-msg">Something went wrong. Please try again later.</p>
          <CardsGrid v-else :items="items" />
        </section>
      </main>
    </div>
  </div>
</template>

<script>
import ActivitiesMenu from './components/ActivitiesMenu.vue';
import Spinner from '@/components/Spinner.vue';
import CardsGrid from '@/components/CardsGrid.vue';

export default {
  name: 'App',
  components: {
    ActivitiesMenu,
    Spinner,
    CardsGrid,
  },
  data() {
    return {
      activeLink: '',
      isFetching: false,
      items: [],
      dataUrl:
        'https://gist.githubusercontent.com/ReemLotfy/4ea8e4b71c4af5f1aa0e321869ea2b0d/raw/c563b15604b04e2f8d052d3d28ab1e17f63db1a0/',
      error: false,
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
    getData() {
      this.isFetching = true;
      this.axios
        .get(`${this.dataUrl}${this.activeLink}-data.json`)
        .then(response => {
          this.items = response.data;
        })
        .catch(err => {
          console.error(err);
          this.error = true;
        })
        .finally(() => {
          this.isFetching = false;
        });
    },
    setActiveLink(link) {
      this.activeLink = link;
    },
  },
};
</script>

<style>
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

#main {
  margin-top: 8px;
}

.Spinner {
  height: 40px;
  width: 40px;
  margin: 0 auto;
  color: var(--primary);
}

.Error-msg {
  font-size: 24px;
  line-height: 24px;
  font-weight: bold;
}
</style>
