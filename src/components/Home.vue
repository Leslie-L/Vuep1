<script setup>
import Header from './Header.vue'
import Layout from './Layout.vue'
import Resume from './Resume/Index.vue'
import Movements from './Movements.vue' 


const amount=null;
</script>
<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume 
        :label="'Ahorro total'"
        :total-amount="100000"
        :amount="amount"
      >
      <template #grapic>graphic</template>
      <template #action>action</template>
      </Resume>
    </template>
    <template #movements>
      <Movements />
    </template>
  </Layout>
</template>
