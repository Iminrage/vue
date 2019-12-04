<template>
  <div id="app">
    <div class="container">
      <section class="section-form">
        <h2 class="title section-form__title">Notes App!</h2>
        <Form
          class="app__form"
          :note="note"
          :error="error"
          @addNote="addNote"
          @clearError="clearError"
        />
      </section>
      <section class="section-notes">
        <NotesFilter
          @noteSearch="query = $event"
          @toggleGrid="grid = !grid"
          :grid="grid"
          placeholder="Найти заметку"
        ></NotesFilter>
        <Notes :grid="grid" :notes="notesFilter" @rmNote="rmNote" />
      </section>
    </div>
  </div>
</template>

<script>
import Form from "./components/Form.vue";
import Notes from "./components/Notes.vue";
import NotesFilter from "./components/NotesFilter.vue";
export default {
  name: "app",
  data() {
    return {
      error: "",
      note: {
        headPlaceholder: "Введите заголовок заметки здесь...",
        head: "",
        bodyPlaceholder: "Введите текст заметки здесь...",
				body: "",
				priority: 0
      },
      grid: true,
      notes: [
        { head: "1st", body: "yeah thats 1st", priority: 0 },
        { head: "2nd", body: "yeah thats 2nd", priority: 1 }
			],
			query: ""
    };
	},
	computed: {
		notesFilter(){
			let newNotes = this.notes;
			if (!this.query) return newNotes;
			let query = this.query.trim().toLowerCase();
			newNotes = newNotes.filter(note=>{
				if (note.head.trim().toLowerCase().indexOf(query) !== -1 || note.body.trim().toLowerCase().indexOf(query) !== -1) return note
			});
			return newNotes;
		}
	},
  methods: {
    clearError() {
      this.error = "";
    },
    addNote() {
      if (!this.note.head) return (this.error = "invalid head");
      this.notes.push({
        ...this.note,
        date: new Date(Date.now()).toLocaleString()
      });
      this.clearError();
      this.note.head = "";
			this.note.body = "";
    },
    rmNote(index) {
      this.notes.splice(index, 1);
    },
  },
  components: {
    Form,
    Notes,
    NotesFilter
  }
};
</script>
