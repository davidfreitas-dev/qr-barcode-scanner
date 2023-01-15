<template>
  <ion-header :translucent="true">
    <ion-toolbar
      class="ion-safe-area-top"
      color="primary"
      style="--border-color: transparent"
    >
      <ion-buttons
        v-if="viewBackButton"
        :class="{'ion-padding-start': isiOS}"
        slot="start"
      >
        <ion-back-button
          defaultHref="home"
          text=""
        ></ion-back-button>
      </ion-buttons>
      <ion-title>My Scanner</ion-title>
    </ion-toolbar>
  </ion-header>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';
import { isPlatform } from '@ionic/vue';
import { IonHeader, IonTitle, IonToolbar, IonButtons, IonBackButton } from '@ionic/vue';

const isiOS = ref(null);

const viewBackButton = ref(false);

onMounted(() => {
  const currentRoute = useRoute().name;
  viewBackButton.value = currentRoute === 'Scanner';
  
  isiOS.value = isPlatform('ios')
}) 
</script>