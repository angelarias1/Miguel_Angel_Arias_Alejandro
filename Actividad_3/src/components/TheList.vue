<script setup lang="ts">
import { ref } from 'vue';
import ItemsVue from './Items.vue';
import Skills from "@/data/Skills";
import type { ISkill } from './interface/ISkill';

const skillInput = ref('');
const passwordInput = ref('');
const skillReactivo = ref(Skills);
const order = ref('asc');

const Ordenar = () => {
  if (order.value === "asc") {
    skillReactivo.value.sort((a, b) => a.id - b.id);
  } else {
    skillReactivo.value.sort((a, b) => b.id - a.id);
  }
}

const isValidEmail = (email: string): boolean => {
  const isUnique = !skillReactivo.value.some(skill => skill.name.toLowerCase() === email.toLowerCase());
  const hasAtSymbol = email.includes('@');
  return isUnique && hasAtSymbol;
}

const isValidPassword = (password: string): boolean => {
  return password.length >= 8;
}

const save = () => {
  if (!skillInput.value.trim() && !passwordInput.value.trim()) {
    return alert('Debes agregar un Correo o una contraseña');
  }

  if (skillInput.value.trim() && !isValidEmail(skillInput.value)) {
    return alert('Error: El correo no es válido, probablemente ya existe o no contiene un "@"');
  }

  if (passwordInput.value.trim() && !isValidPassword(passwordInput.value)) {
    return alert('Error: La contraseña no es válida, debe tener al menos 8 caracteres');
  }

  const nextId = skillReactivo.value.length + 1;
  const newItem: ISkill = {
    id: nextId,
    name: skillInput.value.trim() || passwordInput.value.trim(),
  };

  skillReactivo.value.push(newItem);
  
  skillInput.value = '';
  passwordInput.value = '';
  Ordenar();
}

const remove = (id: number) => {
  const index = skillReactivo.value.findIndex(skill => skill.id === id);
  if (index !== -1) {
    skillReactivo.value.splice(index, 1);
  }
}

const edit = (id: number, newName: string) => {
  const skill = skillReactivo.value.find(skill => skill.id === id);
  if (skill) {
    skill.name = newName;
    Ordenar();
  }
}
</script>

<template>
  <div class="box">
    <input class="input" type="text" placeholder="Agregar Correo" v-model="skillInput" @keyup.enter="save" />
    <input class="input" type="password" placeholder="Agregar Contraseña" v-model="passwordInput" @keyup.enter="save" />
    <select placeholder="Ordenar Lista" v-model="order" @change="Ordenar">
      <option value="asc">Primero</option>
      <option value="desc">Ultimo</option>
    </select>
    <ItemsVue :items="skillReactivo" :remove="remove" :edit="edit" />
  </div>
</template>
