<script setup>
import { Outlet } from "remix-router-vue";
import { IonApp } from '@ionic/vue';
</script>

<template>
  <IonApp>
    <Outlet />
  </IonApp>
</template>