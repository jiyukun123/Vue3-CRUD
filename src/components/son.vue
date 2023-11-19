<script setup>
const props=defineProps({
    car:String,
    money:Number
})

const emit=defineEmits(['changeMoney'])

const buy=()=>{
    emit('changeMoney',5)
}

</script>
<template>
  <div class="son">
    我是son组件 {{ car }} {{ money }}
    <button @click="buy">改变金额</button>
  </div>
</template>
<style>

.son{
   border: 1px solid #000;
   padding: 30px;
}
</style>