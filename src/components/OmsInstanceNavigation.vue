<template>
  <!-- Todo: add translation to the texts once support added in dxp -->
	<ion-card>
		<ion-card-header> 
			<ion-card-subtitle>
				{{ 'Go To OMS' }}
			</ion-card-subtitle> 
			 <ion-card-title>
				{{ appUserState.instanceUrl }}
			</ion-card-title> 
		 </ion-card-header>
		<ion-card-content> 
			{{ 'This is the name of the OMS you are connected to right now. Make sure that you are connected to the right instance before proceeding.' }} -->
		</ion-card-content> 
		<ion-button @click="goToOms(appUserState.userToken, appUserState.instanceUrl)" fill="clear">
			{{ 'Go to OMS' }}
			<ion-icon slot="end" :icon="openOutline" />
		</ion-button>
	</ion-card>
</template>

<script setup lang="ts">
import {IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCardContent, IonButton, IonLabel, IonIcon} from '@ionic/vue'
import {openOutline} from 'ionicons/icons'
import {appContext,goToOms} from '../index'
import {computed} from 'vue'

const store = appContext.config.globalProperties.$store;
const appUserState = computed(() => {
  return {
    instanceUrl: store.getters['user/getInstanceUrl'],
    userToken: store.getters['user/getUserToken']
  }
})
</script>