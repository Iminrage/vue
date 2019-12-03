<template>
  <div class="form">
    <div class="form__input-wrapper">
      <input class="form__input" @focus="focused" v-model="note.head" :placeholder="note.headPlaceholder" type="text" />
      <span class="form__error-message" v-if="error">{{ error }}</span>
    </div>
		<div class="form__input-wrapper">
    <textarea class="form__input form__input--text-area" v-model="note.body" :placeholder="note.bodyPlaceholder" type="text"></textarea>
		</div>
    <button type="submit" class="form__submit" @click="addNote">add</button>
  </div>
</template>



<script>
export default {
  name: "Form",
  props: {
    note: {
      type: Object,
      required: true
    },
    error: {
      type: String,
      required: true
    }
  },
  methods: {
    focused() {
      this.$emit("clearError");
    },
    addNote() {
      this.$emit("addNote", this.note);
    }
  }
};
</script>