<template>
  <ion-button
    class="ion-margin"
    expand="block"
    router-link="/scanner"
  >
    <span>QR and Bar Code Scanner</span>
    <ion-icon
      :icon="scan"
      class="ion-padding-start"
    ></ion-icon>
  </ion-button>
</template>

<script setup>
import { IonButton, IonIcon } from '@ionic/vue';
import { scan } from 'ionicons/icons';
</script>