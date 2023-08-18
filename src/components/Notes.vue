<template>
  <div class="notes">
    <div class="container">
      <div class="notes__top">
        <h2 class="notes__title">{{notes.length > 0 ? 'Barcha eslatmalar' : 'Eslatmalar yoq'}}</h2>

        <button class="notes__btn" @click="grid = !grid">
          <img src="@/assets/img/Vector.svg" alt="" v-if="grid" />
          <img src="@/assets/img/setka.svg" alt="" v-else />
          <span>{{ grid ? "Ro'yhat" : "Setka" }}</span>
        </button>
      </div>

      <div class="notes__list" :class="{active: !grid}">

        <NoteItem
         :grid="grid"
         v-for="note in notes "
         :key="note.id"
         :note="note"
         @changeNote="$emit('changeNote', note.id)"
         @delNote="$emit('delNote', note.id)"
        
         ></NoteItem>

      </div>

    </div>
  </div>
</template>

<script>
import NoteItem from "@/components/NoteItem.vue";

export default {
  components: {
    NoteItem,
  },

  data() {
    return {
      grid: true,
    };
  },

  props: {
    notes: {
      typeof: Array,
      required: true
    }
  }
};
</script>

<style>
.notes {
  margin-top: 30px;
}

.notes__top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.notes__title {
  font-size: 22px;
  line-height: 28px;
  color: #323232;
}

.notes__btn {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15),
    0px 1px 3px rgba(0, 0, 0, 0.3);
  border-radius: 16px;
  width: 120px;
  height: 56px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
}

.notes__btn span {
  font-size: 14px;
  font-family: "Roboto-Medium";
  line-height: 20px;
  color: #6750a4;
}

.notes__list {
  margin-top: 50px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.notes__list.active{
     grid-template-columns: 1fr;
}


</style>