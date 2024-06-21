<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <main>
      <p>{{ labelVisual }}</p>
      <h1>{{ amountCurrency }}</h1>
      <div class="graphic">
        <slot name="graphic"></slot>
      </div>
      <div class="action">
        <slot name="action"></slot>
      </div>
    </main>
</template>
<script setup>
import {defineProps, computed} from 'vue'
const {label,amount,totalAmount} = defineProps({
  label: {
    type: String
  },
  amount:{
    type:Number,
    default:null
  },
  totalAmount:{
    type:Number
  }
})
const currencyFormatter = new Intl.NumberFormat("es-GT", {
        style: "currency",
        currency: "GTQ"
  })
  const amountVisual = computed(()=> amount!=null?amount:totalAmount)
  const labelVisual = computed(()=>{
    if(amount==null){
      return (new Date).toDateString()
    }else{
      return label
    }
  })
  const amountCurrency = computed(()=>{
    return currencyFormatter.format(amountVisual.value)
  })

</script>
<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
}
h1 {
  margin-top: 14px;
  color: var(--brand-green);
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>