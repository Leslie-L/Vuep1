<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="movement">
        <div class="content">
            <h4>{{ title }}</h4>
            <p>{{ description }}</p>
        </div>
        <div class="action">
            <img src="@/assets/trash-icon.svg" alt="Borrar" @click="remove">
            <p :class="{'red':isNegative,'green':!isNegative}">{{ amountCurrency }}</p>
        </div>
    </div>
</template>
<script setup>
import {defineProps, toRefs, computed, defineEmits } from 'vue'

const props = defineProps({
    id:{
        type:Number
    },
    title:{
        type:String
    },
    description:{
        type:String
    },
    amount:{
        type:Number
    }
})
const {id,title,description,amount} = toRefs(props)

const currencyFormatter = new Intl.NumberFormat("es-GT", {
        style: "currency",
        currency: "GTQ"
})
const amountCurrency= computed(()=> currencyFormatter.format(amount.value))
const isNegative = computed(()=>amount.value<0)

const emit = defineEmits(["remove"])
const remove=()=>{
    emit("remove",id.value)
}
</script>
<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  color: black;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
  font-size: larger;
  font-weight: bold;
  color: rgb(44, 44, 110);
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
    color: red;
    font-weight: bold;
}
.green {
    color: green;
    font-weight: bold;
}
</style>