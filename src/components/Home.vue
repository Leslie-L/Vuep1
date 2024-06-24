<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, computed,onMounted } from 'vue'
import Header from './Header.vue'
import Layout from './Layout.vue'
import Graphic from  './Graphic.vue'
import Resume from './Resume/Index.vue'
import Movements from './Movements/Index.vue'
import Action from './Action.vue'

const movements = ref([])
onMounted(() => {
  const movementsFromLocalStorage = localStorage.getItem('movements');
  if (movementsFromLocalStorage) {
    
    movements.value = JSON.parse(movementsFromLocalStorage);
  }
});
const amounts = computed(()=>{
  const lastDays = movements.value
        .filter(m => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);

          return m.time > oldDate;
        })
        .map(m => m.amount);
      
      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i +1);

        return lastMovements.reduce((suma, movement) => {
          return suma + movement
        }, 0);
      });
})

const amount = null
const totalAmount = computed(()=>{
  return movements.value.reduce((acc,current)=>{
    return acc+current.amount},0)
})

const remove = (id)=>{
  const index=movements.value.findIndex(m=>m.id===id);
  movements.value.splice(index,1)
  save();
}
const create = (movement)=>{
  movements.value.push(movement)
  save();
}
const save=()=>{
  localStorage.setItem('movements', JSON.stringify(movements.value));
}
//const amounts = [100, 200, 500, -400, 200, -600, 20, 500]
</script>
<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume :label="'Ahorro total'" :total-amount="totalAmount" :amount="amount">
        <template #graphic>
          <Graphic :amounts="amounts" />
        </template>
        <template #action>
          <Action @create="create" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" @remove="remove" />
    </template>
  </Layout>
</template>
