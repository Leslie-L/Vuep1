<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import {computed} from 'vue'
import Header from './Header.vue'
import Layout from './Layout.vue'
import Graphic from  './Graphic.vue'
import Resume from './Resume/Index.vue'
import Movements from './Movements/Index.vue'
import Action from './Action.vue'

const movements = [
  {
    id: 1,
    title: 'Movimiento',
    description: 'Deposito de salario',
    amount: 1000,
    time: new Date("12-06-2024")
  },
  {
    id: 2,
    title: 'Movimiento 1',
    description: 'Deposito de honorarios',
    amount: 500,
    time: new Date("12-06-2024")
  },
  {
    id: 3,
    title: 'Movimiento 3',
    description: 'Comida',
    amount: -100,
    time: new Date("12-06-2024")
  },
  {
    id: 4,
    title: 'Movimiento 4',
    description: 'Colegiatura',
    amount: 1000,
    time: new Date("12-06-2024")
  },
  {
    id: 5,
    title: 'Movimiento 5',
    description: 'Reparación equipo',
    amount: 1000,
    time: new Date("12-01-2024")
  }
  
]
const amounts = computed(()=>{
  const lastDays = movements
        .filter(m => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);

          return m.time > oldDate;
        })
        .map(m => m.amount);
      
      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i);

        return lastMovements.reduce((suma, movement) => {
          return suma + movement
        }, 0);
      });
})

const amount = null
//const amounts = [100, 200, 500, -400, 200, -600, 20, 500]
</script>
<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume :label="'Ahorro total'" :total-amount="100000" :amount="amount">
        <template #graphic>
          <Graphic :amounts="amounts" />
        </template>
        <template #action>
          <Action />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" />
    </template>
  </Layout>
</template>
