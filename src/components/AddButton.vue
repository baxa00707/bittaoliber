<template>
  
  <button class="add__btn" @click="$emit('openModal')">
    <img src="@/assets/img/edit.svg" alt="">

  </button>
</template>

<script>
export default {

}
</script>

<style>

.add__btn{
    border-radius: 16px;
    background: linear-gradient(0deg, rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11)), #FFFBFE;
    width: 56px;
    height: 56px;
    position: fixed;
    right: 30px;
    bottom: 30px;
}

</style>