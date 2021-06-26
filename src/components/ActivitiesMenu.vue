<template>
  <nav>
    <ul class="Activity__List">
      <li
        v-for="(activity, idx) in activities"
        :key="idx"
        class="Activity__Item"
        @click="setActiveLink(activity.label)"
      >
        <button type="button" class="Activity__Btn">
          <span class="Activity__Icon">
            <icon-base width="30" height="30" :icon-name="activity.label" :iconColor="'#3db2f3'">
              <icon-food v-if="activity.label === 'food'" />
              <icon-golf v-if="activity.label === 'golf'" />
              <icon-arts v-if="activity.label === 'arts'" />
            </icon-base>
          </span>
          <span>{{ activity.name }}</span>
        </button>
      </li>
    </ul>
  </nav>
</template>

<script>
import IconBase from '@/components/IconBase.vue';
import IconGolf from '@/components/icons/IconGolf.vue';
import IconFood from '@/components/icons/IconFood.vue';
import IconArts from '@/components/icons/IconArts.vue';

export default {
  name: 'ActivitiesMenu',
  components: {
    IconBase,
    IconGolf,
    IconFood,
    IconArts,
  },
  data() {
    return {
      activities: [
        {
          name: 'Food',
          label: 'food',
          icon: IconFood,
        },
        {
          name: 'Golf',
          label: 'golf',
          icon: IconGolf,
        },
        {
          name: 'Arts & designs',
          label: 'arts',
          icon: 'art-icon',
        },
      ],
    };
  },
  mounted() {
    this.setActiveLink(this.activities[0].label);
  },
  methods: {
    setActiveLink(link) {
      this.$emit('active-link', link);
    },
  },
};
</script>

<style lang="postcss" scoped>
.Activity__List {
  list-style-type: none;
  padding: 0;
}

.Activity__Item {
  display: inline-block;
  margin: 0 10px;
}

.Activity__Btn {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: transparent;
  border: none;
}

.Activity__Btn:hover {
  cursor: pointer;
}

.Activity__Icon {
  background-color: white;
  padding: 16px;
  border-radius: 50%;
  border: 8px solid var(--primary-light);
  margin-block-end: 4px;
  position: relative;
}
</style>
