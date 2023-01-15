<template>
  <ion-page>
    <HeaderTop />

    <ion-content :fullscreen="true">
      <div id="container">
        <ion-title
          v-if="barCode"
          class="ion-text-center"
        >
          {{ barCode }}
        </ion-title>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup>
import { ref } from 'vue'
import { IonContent, IonPage, IonTitle, onIonViewDidEnter, onIonViewWillLeave } from '@ionic/vue';
import { BarcodeScanner } from '@capacitor-community/barcode-scanner'
import { isPlatform } from '@ionic/vue'
import HeaderTop from '../components/HeaderTop.vue'

const barCode = ref(null)

const checkPermission = async () => {
  const status = await BarcodeScanner.checkPermission({ force: true });
  
  if (status.granted) {
    return true;
  }

  if (status.denied) {
    const c = confirm('Deseja permitir o uso da camera por este app nas configurações do dispositivo?');
    
    if (c) {
      BarcodeScanner.openAppSettings();
    }

    return true;
  }

  return false;
}

const startScan = async () => {
  const allowed = await checkPermission();

  if (allowed) {  
    document.querySelector('body').classList.add('scanner-active');

    const result = await BarcodeScanner.startScan();

    if (result.hasContent) {
      barCode.value = result.content
      stopScan();
    }
  }
}

const stopScan = () => {
  document.querySelector('body').classList.remove('scanner-active');

  BarcodeScanner.stopScan();
}

onIonViewDidEnter(() => {
  if (isPlatform('ios') || isPlatform('android')) {
    startScan()
  }
});

onIonViewWillLeave(() => {
  if (isPlatform('ios') || isPlatform('android')) {
    stopScan()
  }
});
</script>