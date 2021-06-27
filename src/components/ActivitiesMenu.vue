<template>
  <nav>
    <ul class="Activity__List">
      <li
        v-for="(activity, idx) in activities"
        :key="idx"
        class="Activity__Item"
        @click="setActiveLink(activity.label)"
      >
        <button type="button" class="Activity__Btn" :class="{ Selected: selectedActivity === activity.label }">
          <span class="Activity__Icon">
            <icon-base width="40" height="40" :icon-name="activity.label">
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
      selectedActivity: '',
    };
  },
  mounted() {
    this.setActiveLink(this.activities[0].label);
  },
  methods: {
    setActiveLink(link) {
      this.selectedActivity = link;
      this.$emit('active-link', link);
    },
  },
};
</script>

<style lang="postcss" scoped>
.Activity__List {
  list-style-type: none;
  padding: 0;
  margin-block-end: 48px;
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
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70px;
  height: 70px;
  padding: 6px;
  margin-block-end: 6px;
  background-color: white;
  border-radius: 50%;
  border: 8px solid var(--primary-light);
}

.Selected > .Activity__Icon {
  background-color: var(--primary);
  border: 2px dotted var(--primary);
  padding: 14px;
  background-clip: content-box;
}

.Selected > .Activity__Icon svg {
  color: white;
}

span:last-of-type {
  font-size: 14px;
}

svg[aria-labelledby='food'] {
  margin-right: -6px;
  margin-bottom: -6px;
}

svg[aria-labelledby='golf'] {
  margin-right: -16px;
}
</style>
