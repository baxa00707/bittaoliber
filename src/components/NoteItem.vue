<template>

<div class="notes__item">

    <div class="notes__item-top" :class="{between: !grid}">
       <h3 class="notes__item-title">{{note.title}}</h3>
       <p class="notes__item-date">{{note.date}}</p>
    </div>

    <p class="notes__item-text">{{note.descr}}</p>

    <div class="notes__item-btns">

        <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
            <img src="@/assets/img/edit.svg" alt="">
            <span>O'ZGARTIRISH</span>
        </button>

        <button class="notes__item-btn del" @click="$emit('delNote' , note.id)">
            <img src="@/assets/img/delete.svg" alt="">
            <span>O'СHIRISH</span>
        </button>

    </div>


</div>
  
</template>

<script>
export default {

    props: {
        grid: Boolean,
        note: Object 
    }

}
</script>

<style>

.notes__item{
  background: linear-gradient(0deg, rgba(103, 80, 164, 0.05), rgba(103, 80, 164, 0.05)), #FFFBFE;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3), 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
  border-radius: 16px;
  padding: 16px 16px 28px 16px;
}

.notes__item-title{
    font-family: 'Roboto-Medium';
    line-height: 24px;
}


.notes__item-date{
    color: #CAC4D0;
    font-size: 14px;
    line-height: 20px;
}

.notes__item-text{
    font-size: 14px;
    line-height: 20px;
    font-family: 'Roboto-Regular';
    color: #49454F;
    margin: 16px 0 30px;
}

.notes__item-btns{
    display: flex;
    justify-content: flex-end;
    gap: 15px;
}


.notes__item-btn{
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px;
    border-radius: 5px;
}


.notes__item-btns span {
    font-size: 14px;
    line-height: 20px;
    font-family: 'Roboto-Medium';
}

.edit{
    color: #6750A4;
}

.edit:hover{
    background: #E6DDFF;
}
.del{
    color: #CF1B1B;
}

.del:hover{
 background: #FFE1E1;
}

.between{
    display: flex;
    justify-content: space-between;
    align-items: center;
}




</style>