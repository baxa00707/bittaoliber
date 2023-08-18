<template>

<Transition name = "modal">

<div class="modal" @click="closeModal">

    <div class="modal__block" @click.stop>
        <h2 class="modal__title">
            {{ edit ? 'Eslatmalar tahrirlash' : 'Eslatma qo`shish'}}
        </h2>

        <div class="modal__inputs">

            <label>
                <span>Title</span>
                <input type="text" v-model="title">
            </label>

            <label>
                <span>Content</span>
                <textarea v-model="descr"></textarea>
            </label>

        </div>

        <div class="modal__btns">
            <button class="modal__btn cancel" @click="closeModal">BEKOR QILISH</button>
            <button v-if="!edit" class="modal__btn add" @click="addNote">QO'SHISH</button>
            <button v-else class="modal__btn add" @click="changeNote">O'ZGARTIRISH</button>
        </div>


    </div>

</div>

</Transition>
  
</template>

<script>
export default {

    data(){
        return{
          title: ' ',
          descr: ' ',
          id: this.currentId
        }
    },
  


    props:{
        currentId: Number,
        edit:Boolean,
        editNote: Object
    },

    methods: {
        closeModal(){
            this.$emit('closeModal', false)
        },

        addNote(){

            if(this.title != ' ' && this.descr  != ' '){
            const item = {
                id: this.id++,
                title: this.title,
                descr: this.descr,
                date: new Date().toLocaleDateString()
            }

            this.$emit('addNote', item),
            this.title= ' ';
            this.descr = ' ';
        }
      },

      changeNote(){
         if(this.title != '' && this.descr != ''){
            const editedNote = {
                id: this.editNote.id,
                title: this.title ,
                descr: this.descr,
                date: new Date().toLocaleString()
            }

            this.$emit('editedNote', editedNote)
            this.closeModal(),
            this.title = '' ,
            this.descr = '' 

         }
      }
     }

}
</script>

<style>

.modal{
    background: rgba(0, 0, 0, 0.35);
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 999;
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal__block{
   background: linear-gradient(0deg, rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11)), #FFFBFE;
   border-radius: 28px;
   max-width: 312px;
   width: 100%;
   padding: 24px;
}

.modal__title{
    color: #1C1B1F;
    font-family: 'Roboto-Regular';
    font-size: 24px;
    line-height: 32px;
    margin-bottom: 16px;
}

.modal__inputs{
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.modal__inputs label {
    position: relative;
}


.modal__inputs span {
    position: absolute;
    left: 16px;
    top: 8px;
    font-size: 12px;
    line-height: 16px;
    color: #6750A4;
}

.modal__inputs input , 
.modal__inputs textarea {
    background: #e7e0ec;
    border-radius: 4px;
    width: 100%;
    border: none;
    outline: none;
    padding: 23px 0 9px 16px;
    line-height: 24px;
    border-bottom: 1px solid black;
    resize: none;
}

.modal__btns{
    display: flex;
    justify-content: flex-end;
    gap: 10px;
    margin-top: 25px;
}

.modal__btn{
    font-size: 14px;
    line-height: 20px;
    font-family: 'Roboto-Medium';
    transition: 0.5s;
    padding: 10px 12px;
    background: transparent;
}


.cancel{
    color: #CF1B1B;
}

.cancel:hover{
    background: #ffe1e1;
}


.add{
    color: #6750A4;
}

.add:hover{
    background: #E6DDFF;
}


.modal-enter-active,
.modal-leave-active {
  transition:  0.5s linear;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.5);
}
</style>