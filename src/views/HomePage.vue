<template>
  <ion-page>
    <HeaderTop />

    <ion-content :fullscreen="true">
      <div id="container">
        <ScannerButton />
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup>
import { IonContent, IonPage } from '@ionic/vue';
import HeaderTop from '../components/HeaderTop.vue'
import ScannerButton from '../components/ScannerButton.vue'
</script>