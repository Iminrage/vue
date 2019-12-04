<template>
  <ul class="notes">
    <li
      v-for="(item, index) in notes"
      class="notes__item"
      :class="[isGrid, currentPriority(item.priority)]" 
      :key="index"
    >
      <button class="notes__close" @click="rmNote(index)">X</button>
      <h3 class="notes__title">{{ item.head }}</h3>
      <p class="notes__descr">{{ item.body }}</p>
      <span class="notes__time">{{ item.date }}</span>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Notes",
  props: {
    notes: {
      type: Array,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    isGrid() {
      return this.grid && "notes__item--grid";
    }
  },
  methods: {
    rmNote(index) {
      this.$emit("rmNote", index);
		},
    currentPriority(index) {		
      if (index > 0) {
        return index === 1 ? "notes__item--yellow" : "notes__item--red";
      }
    }
  }
};
</script>