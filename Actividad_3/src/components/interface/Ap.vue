<!-- App.vue -->
<template>
    <div id="app">
      <LoginComponent />
      <RegisterComponent />
      <UserDataTable />
    </div>
  </template>
  
  <script>
  import LoginComponent from './components/LoginComponent.vue';
  import RegisterComponent from './components/RegisterComponent.vue';
  import UserDataTable from './components/UserDataTable.vue';
  
  export default {
    components: {
      LoginComponent,
      RegisterComponent,
      UserDataTable,
    },
  };
  </script>
  
  <style>
  /* Estilos globales de la aplicación */
  </style>
  