<script setup lang="ts">
import type { ISkill } from './interface/ISkill';
import { ref } from 'vue';

const props = defineProps<ISkill>();
const check = ref(false)
const classItem = ref('item') 
const checkSelect =() =>{
    if(check.value){
        classItem.value= 'item check';
    }else{
        classItem.value= 'item';
    }
}
</script>

<template>
    <div :class="classItem">
        <input type="checkbox" v-model="check" @change="checkSelect"/>
        <span>   {{ props.id  }}. {{props.name }}</span>
    </div>
</template>
