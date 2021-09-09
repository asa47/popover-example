<template>
  <ion-page>
    <ion-content class="ion-padding">
      <ion-button @click="openPopover">Open Popover</ion-button>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonPage, IonButton, popoverController } from '@ionic/vue';
import { defineComponent } from 'vue';
import Popover from './Popover.vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonPage,
    IonButton
  },
  setup() {
    async function openPopover(ev: Event) {
      const popover = await popoverController
        .create({
          component: Popover,
          cssClass: 'popover-class',
          event: ev,
          translucent: false,
          showBackdrop: true,
          backdropDismiss: true
        });
      await popover.present();

      const { role } = await popover.onDidDismiss();
      console.log('onDidDismiss resolved with role', role);
    }
    return {
      openPopover
    }
  }
});
</script>

<style scoped>
ion-content {
  --background: #ffca22;
}
</style>