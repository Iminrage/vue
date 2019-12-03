<template>
  <ul class="notes">
    <li class="notes__item" :class="grid && 'notes__item--grid'" v-for="(item, index) in notes" :key="index">
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
  methods: {
    rmNote(index) {	
      this.$emit("rmNote", index);
    }
  }
};
</script>