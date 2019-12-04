<template>
  <form class="form">
    <div class="form__input-wrapper">
      <input
        class="form__input"
        @focus="focused"
        v-model="newNote.head"
        :placeholder="note.headPlaceholder"
        type="text"
      />
      <div class="form__priority-picker">
        <button
          type="button"
          class="form__priority"
          :class="`${newNote.priority === 1 && 'form__priority--yellow'} ${newNote.priority === 2 && 'form__priority--red'}`"
          @click="setNewPriority"
        >&#33;</button>
      </div>
      <span class="form__error-message" v-if="error">{{ error }}</span>
    </div>
    <div class="form__input-wrapper">
      <textarea
        class="form__input form__input--text-area"
        v-model="newNote.body"
        :placeholder="note.bodyPlaceholder"
        type="text"
      ></textarea>
    </div>
    <button type="submit" class="form__submit" @click="addNote" @submit="addNote">add</button>
  </form>
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
  data() {
    return {
      newNote: this.note
    };
  },
  methods: {
    setNewPriority() {
      this.newNote.priority < 2
        ? this.newNote.priority++
        : (this.newNote.priority = 0);
    },
    focused() {
      this.$emit("clearError");
    },
    addNote(e) {
      e.preventDefault();
      this.$emit("addNote", this.newNote);
    }
  }
};
</script>