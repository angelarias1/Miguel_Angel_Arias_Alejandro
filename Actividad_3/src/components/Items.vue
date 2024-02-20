<template>
    <div>
      <div v-for="(item, index) in items" :key="index">
        <span>{{ item.name }}</span>
        <button @click="editItem(item.id)">Editar</button>
        <button @click="removeItem(item.id)">Eliminar</button>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import type { PropType } from 'vue';
  
  const props = defineProps({
    items: {
      type: Array as PropType<ISkill[]>,
      required: true
    },
    remove: {
      type: Function as PropType<(id: number) => void>,
      required: true
    },
    edit: {
      type: Function as PropType<(id: number, newName: string) => void>,
      required: true
    }
  });
  
  const removeItem = (id: number) => {
    props.remove(id);
  }
  
  const editItem = (id: number) => {
    const newName = prompt('Ingrese el nuevo Correo:');
    if (newName !== null) {
      props.edit(id, newName);
    }
  }
  </script>
  