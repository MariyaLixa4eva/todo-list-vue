<template>
<div class="all">
    <div class="container">
      <h1>{{ title }}</h1>
      <div class="notes-header">
        <Search :value="search" @search="search = $event"/>
        <div class="icons">
          <svg :class="{active: grid}" @click="grid = true" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
          <svg :class="{active: !grid}" @click="grid = false" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
        </div>
      </div>
      <Message
      v-if="message"
      :message="message"
      />
      <NewNote
      :note="note"
      @addNote="addNote"
      />
      
      <Notes
      :notes="notesFilter"
      @remove="removeNote"
      :grid="grid"
      />
    </div>
</div>
</template>

<script>
import Message from "@/components/Message.vue";
import NewNote from "@/components/NewNote.vue";
import Notes from "@/components/Notes.vue";
import Search from "@/components/Search.vue";
export default {
  components: {
    Message,
    NewNote,
    Notes,
    Search,
  },
  data() {
    return {
      title: "Список заметок",
      message: null,
      search: '',
      grid: true,
      note: {
        title: "",
        desc: "",
      },
      notes: [
        {
          title: "первая заметка",
          desc: "описание первой заметки",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "вторая заметка",
          desc: "описание второй заметки",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "третья заметка",
          desc: "описание третьей заметки",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },
  computed:{
    notesFilter() {
      let array = this.notes,
      search = this.search
      if (!search) {
        return array
      }
      search = search.trim().toLocaleLowerCase()
      array = array.filter(function(item) {
        if (item.title.toLocaleLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      return array
    }
  },
  methods: {
    addNote() {
      let { title, desc } = this.note;
      if (title === "" || desc === "") {
        this.message = "Ошибка, введите данные";
        return false;
      }
      this.notes.push({
        title,
        desc,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.note.title = "";
      this.note.desc = "";
      this.message = null;
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  },
};
</script>

<style scoped>
.all {
  padding: 15px;
  max-height: 80%;
  max-width: 90vw;
  margin: 0 auto;
  margin-top: 20px;
  margin-bottom: 20px;
  background-color: rgba(0, 0, 0, 0.3);
  box-shadow: inset 0 0 0.5em 0 #F2E3DB, 0 0 0.5em 0 #F2E3DB;
  border-radius: 15px;
  -webkit-backdrop-filter: blur(5px);
  backdrop-filter: blur(5px);
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 15px;
}
.container h1 {
  margin-left: 15px;
  font-size: 40px;
  color: #F2E3DB;
  text-align: center;
}
.container h1::before {
  content: "\2714 ";
  color: #E86A33;
}
.notes-header {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  color: #F2E3DB;
  gap: 10px;
  width: 90%;
}
.icons {
display: flex;
justify-content: center;
}

.notes-header svg {
  margin-right: 15px;
}
.notes-header svg.active {
  color: #E86A33;
}
@media all and (max-width:500px) {
  .all {
  padding: 10px;
  max-height: 80%;
  max-width: 90vw;
}
.notes-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
}
.icons {
display: flex;
justify-content: center;
width: 100%;
}
.notes-header svg {
  margin-right: 0;
  margin: 10px;
}
}
</style>
