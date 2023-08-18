<template>

<Navbar
@searchValue="search=$event"

></Navbar>

<Notes
 :notes="filterNotes"
 @delNote="deleteNote"
 @changeNote="changeNote"
 ></Notes>

<Modal
 :edit="edit"
 :editNote ="editNote"
 @addNote ="addNote"
 :currentId="currentId"
 v-show="modalOpen"
 @closeModal="closeModal"
 @editedNote ="editedNote"

  ></Modal>

<AddButton @openModal = "openModal"></AddButton>
  
</template>

<script>

import Navbar from '@/components/Navbar.vue'
import Notes from '@/components/Notes.vue'
import Modal from '@/components/Modal.vue'
import AddButton from '@/components/AddButton.vue'

export default {
   components: {
     Navbar,
     Notes,
     Modal,
     AddButton
   },

   data(){
    return{
      currentId:1,
      modalOpen: false,
      notes: [ ],
      edit: false,
      editNote: {},
      search: ''

    }
   },

   created(){
      this.getNotes()
   },

   computed: {
       filterNotes(){
         return  this.search ? this.notes.filter(note => note.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes;
       }
   },

   methods: {
    openModal(){
      this.modalOpen = true
    },

    closeModal(status){
       this.modalOpen = status
       setTimeout(() => this.edit = false, 500)
       
    },
    addNote(item){
        this.notes.push(item)  
        this.modalOpen = false
    },

    deleteNote(id){
       let index = this.notes.findIndex(note => note.id == id)
       this.notes.splice(index, 1)
    },

    getNotes(){
      const localeNotes = localStorage.notes
       if(localeNotes) {
          this.notes = JSON.parse(localeNotes)
       }
    },

    changeNote(id){
       this.edit = this.modalOpen = true;
       let pickedNote = this.notes.find(note => note.id == id)
       this.editNote = pickedNote 
    },

    editedNote(noteEdited){
       this.notes.forEach(note => {
         if(note.id == noteEdited.id){
             note.title = noteEdited.title 
             note.descr = noteEdited.descr
             note.date = noteEdited.date
         }
       })
    }
   },

   watch: {
    notes: {
       handler(newNotes){
          localStorage.notes = JSON.stringify(this.notes)
       },
       deep: true
    },

   }

   
}
</script>

<style>

</style>