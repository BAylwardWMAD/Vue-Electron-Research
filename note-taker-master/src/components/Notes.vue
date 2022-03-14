<template>
  <div class="note">
    <!-- Add a new Note Button -->
    <button class="my-4 mx-lg-3 rounded-pill" @click="isCreating = !isCreating">
      <i class="fas fa-plus fs-3"></i>
    </button>
    <!-- Main note area -->
    <div class="note-header ps-2 my-4">
      <div class="noteList me-lg-5 p-lg-3 mb-2">
        <h3 class="text-center">My Notes</h3>
        <ul class="note-item-list mx-auto">
          <li
            class="note-item d-flex align-items-center py-2 border-bottom fw-bold justify-content-between"
            v-for="n in noteList"
            :key="n"
          >
            <span class="btn text-white text-start" @click="queryNote(n.id)">{{
              n.title
            }}</span>
            <button class="btn bg-danger" @click="deleteNote(n.id)">X</button>
          </li>
        </ul>
      </div>
      <div class="note-display text-end" :class="isDisplayed ? 'display' : ''">
        <h4 ref="title">Title</h4>
        <p ref="desc">Description</p>
        <button class="me-3" ref="id" @click="editNote">Edit</button>
        <button @click="isDisplayed = false">Close Note</button>
      </div>
    </div>
    <!-- Note creation/edit form -->
    <div class="noteForm text-center pb-5" :class="isCreating ? 'display' : ''">
      <label class="form-label">Title:</label><br />
      <input
        type="text"
        class="form-control"
        minlength="2"
        v-model="note.title"
      />
      <label class="form-label">Description:</label>
      <textarea class="form-control" v-model="note.description"></textarea>
      <button class="mt-3 me-3" @click="addNote">Save</button>
    </div>
  </div>
</template>

<script>
import Note from "./Note.js";

/*eslint-disable*/
// const fs = require("fs");
// const path = require("path");

// let pathToApp = __dirname.substring(0, __dirname.indexOf("node_modules"));
// let pathToDataFile = path.resolve(pathToApp, "src/assets/data.json");

export default {
  name: "MyNotes",
  data: function () {
    return {
      isDisplayed: false,
      isCreating: false,
      note: new Note(),
      noteList: [],
    };
  },
  methods: {
    addNote() {
      this.note.id = this.note.id ? this.note.id : this.createId();

      let index = this.noteList.findIndex((n) => n.id == this.note.id);
      if (index == -1) this.noteList.push(this.note);
      else this.noteList[index] = this.note;

      this.note = new Note();
      this.isCreating = false;
      this.isDisplayed = false;
      this.saveList();
    },
    createId() {
      if (this.noteList.length == 0) return 1;
      return this.noteList[this.noteList.length - 1].id + 1;
    },
    queryNote(id) {
      let queriedNote = this.noteList.find((n) => n.id == id);

      if (queriedNote) {
        this.isDisplayed = true;
        this.$refs.title.innerText = queriedNote.title;
        this.$refs.desc.innerText = queriedNote.description;
        this.$refs.id.value = queriedNote.id;
      }
    },
    editNote() {
      let id = this.$refs.id.value;
      this.note = this.noteList.find((n) => n.id == id);
      this.isCreating = true;
    },
    deleteNote(id) {
      let index = this.noteList.findIndex((n) => n.id == id);
      this.noteList.splice(index, 1);
      this.isDisplayed = false;
      this.saveList();
    },
    saveList() {
      // fs.writeFile(
      //   pathToDataFile,
      //   JSON.stringify(this.noteList),
      //   function (err) {
      //     if (err) {
      //       console.log(err);
      //       return;
      //     }
      //     console.log("File saved");
      //   }
      // );
    },
  },
  beforeMount() {
    //load from our file
    // fs.readFile(pathToDataFile, "utf-8", (err, data) => {
    //   if (err) console.log(err);
    //   else this.noteList = JSON.parse(data);
    // });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.note-header {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  align-items: center;
}
.noteForm {
  padding: 0 2rem 2rem 2 rem;
  opacity: 0;
  transition: 200ms ease;
  max-width: 400px;
  margin: 0 auto;
}
.noteForm.display {
  opacity: 1;
}
.noteForm * {
  margin: 0 auto;
}
.noteList ul {
  list-style: none;
  padding: 0;
}
.noteList {
  min-width: 300px;
  text-align: start;
}
.note-item-list {
  max-width: 350px;
}
.note-display {
  opacity: 0;
  transition: 200ms ease;
  text-align: start;
  max-width: 450px;
  width: 450px;
  word-wrap: break-word;
}
.note-display.display {
  opacity: 1;
}
input[type="text"],
textarea {
  width: 300px;
}
button {
  padding: 0.5rem 1rem;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: 600;
  border: none;
  background: #2c3e7f;
  border-radius: 10px;
  transition: 300ms ease;
  color: #ddd;
}
button:hover {
  background: #2c3eff;
  color: #fff;
  transform: translateY(2px);
}
</style>
