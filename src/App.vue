<template>
<!-- <button @click="useChannel.getList">获取数据</button>

<li v-for=" item in useChannel.channelList" :key="item.id">{{ item.name }}</li>



父组件
{{ money }}
<button @click="getmoney()">修改</button>
<Son car="123" :money="money" 
 @changeMoney="changeFn"
></Son>
 -->
<watch/>
</template>

<script setup>
const useChannel =useChannelStore()
import watch from '@/components/watch.vue'
import {useChannelStore} from '@/store/channel.js'
import {ref} from 'vue'
//import Son from '@/components/son.vue'



const money=ref(100)
const getmoney=()=>{
    money.value++
}

const changeFn=(t)=>{
    money.value+=t
}


</script>

<style>

</style>