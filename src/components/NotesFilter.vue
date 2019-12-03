<template>
  <div class="filters">
    <input class="filters__input" type="text" v-model="property" :placeholder="placeholder" />
    <div class="filters__btns">
      <button class="filters__btn filters__btn--grid" :class="grid && 'filters__btn--active'" @click="setGrid(true)">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <rect x="3" y="3" width="7" height="7" />
          <rect x="14" y="3" width="7" height="7" />
          <rect x="14" y="14" width="7" height="7" />
          <rect x="3" y="14" width="7" height="7" />
        </svg>
      </button>
      <button class="filters__btn filters__btn--stroke" :class="!grid && 'filters__btn--active'" @click="setGrid(false)">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <line x1="8" y1="6" x2="21" y2="6" />
          <line x1="8" y1="12" x2="21" y2="12" />
          <line x1="8" y1="18" x2="21" y2="18" />
          <line x1="3" y1="6" x2="3" y2="6" />
          <line x1="3" y1="12" x2="3" y2="12" />
          <line x1="3" y1="18" x2="3" y2="18" />
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NotesFilter",
  props: {
    placeholder: {
      type: String,
      required: false
    },
    property: {
      type: String
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    setGrid(isGrid) {
      if (this.grid) {
        !isGrid && this.$emit("toggleGrid");
      } else {
        isGrid && this.$emit("toggleGrid");
      }
    }
  }
};
</script>