<template>
  <header class="header">

    <Transition name="header__notes">
    <div class="header__notes" v-show="header === true">
      <button class="header__lang">UZ</button>
      <h1 class="header__title">Eslatmalar</h1>
      <button class="header__search" @click="header = false">
        <img src="@/assets/img/search.svg" alt="" />
      </button>
    </div>
    </Transition>

   <Transition name="header__form">

    <div class="header__form" v-show="header === false">

        <button class="header__back" @click="header = true , search= ''">
            <img src="@/assets/img/arrow.svg" alt="">
        </button>

        <input type="text" placeholder="Qidirish..." class="header__input" v-model="search">

        <button class="header__close" @click="search = ''">
            <img src="@/assets/img/close.svg" alt="">
        </button>


    </div>
  </Transition>




  </header>
</template>

<script>
export default {
    data(){
        return{
            header: true,
            search: ''
        }
    },

    watch: {
      search(val){
        this.$emit('searchValue', val)
      }
    }
};
</script>

<style>

.header {
  background: #f3edf7;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25), 0px 1px 3px rgba(0, 0, 0, 0.3);
  padding: 18px 20px;
  height: 70px;
  overflow: hidden;
}

.header__notes,
.header__form{
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.header__lang{
    font-size: 22px;
    font-weight: bold;
}

button{
    border: none;
}

.header__title{
    font-size: 22px;
    line-height: 28px;
}

.header__input{
    width: 90%;
    display: block;
    background: transparent;
    border: none;
    outline: none;
}

.header__notes-enter-active,
.header__notes-leave-active {
  transition:  0.5s linear;
}

.header__notes-enter-from,
.header__notes-leave-to {
  opacity: 0;
  transform: translateY(-200px);
}

.header__notes-enter-to,
.header__notes-leave-from {
  opacity: 1;
  transform: translateY(0px);
}

/*---------------------------------- */


.header__form-enter-active,
.header__form-leave-active {
  transition:  0.5s linear;
}

.header__form-enter-from,
.header__form-leave-to {
  opacity: 0;
  transform: translateY(200px);
}

.header__form-enter-to,
.header__form-leave-from {
  opacity: 1;
  transform: translateY(0px);
}

</style>