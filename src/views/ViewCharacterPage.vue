<template>
    <ion-page>
      <ion-header :translucent="true">
        <ion-toolbar>
          <ion-buttons slot="start">
            <ion-back-button :text="getBackButtonText()" default-href="/"></ion-back-button>
          </ion-buttons>
        </ion-toolbar>
      </ion-header>
  
    <ion-content :fullscreen="true" v-if="character">
        <ion-card>
    <ion-card-header>
      <ion-card-title>{{ character.id }} {{ character.name }}</ion-card-title>
      <ion-card-subtitle>{{ character.species }} {{  character.gender  }} {{ character.status  }}</ion-card-subtitle>
    </ion-card-header>
    <img style="margin:auto; padding: 5px;" :src="character.image"/>
    <ion-card-content>
      <strong>Location</strong> :{{ character.location.name }} <br>
      <strong> Origin </strong> :{{ character.origin.name }}
    </ion-card-content>
  </ion-card>
        
      </ion-content>
    </ion-page>
  </template>
  
  <script setup lang="ts">
  import { useRoute } from 'vue-router';
  import {
    IonBackButton,
    IonButtons,
    IonContent,
    IonHeader,
    IonPage,
    IonToolbar,
    IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle
  } from '@ionic/vue';
  import { ref, onMounted } from 'vue';
  
  const getBackButtonText = () => {
    const win = window as any;
    const mode = win && win.Ionic && win.Ionic.mode;
    return mode === 'ios' ? 'Characters' : '';
  };
  
  const route = useRoute();
  const character = ref(null);
  
  const fetchCharacter = async (id: number) => {
    try {
      const response = await fetch(`https://rickandmortyapi.com/api/character/${id}`);
      const data = await response.json();
      character.value = data; // Asignamos los datos del personaje
     // console.log(character.value.id);
  
    } catch (error) {
      console.error('Error fetching character:', error);
    }
  };
  
  onMounted(() => {
    const id = parseInt(route.params.id as string, 10);
    fetchCharacter(id); // Llamamos a la función para obtener los datos del personaje
  
  
  });
  </script>
  
  <style scoped>
  ion-item {
    --inner-padding-end: 0;
    --background: transparent;
  }
  
  ion-label {
    margin-top: 12px;
    margin-bottom: 12px;
  }
  
  ion-item h2 {
    font-weight: 600;
  
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  
  ion-item .date {
    align-items: center;
    display: flex;
  }
  
  ion-item ion-icon {
    font-size: 42px;
    margin-right: 8px;
  }
  
  ion-item ion-note {
    font-size: 0.9375rem;
    margin-right: 12px;
    font-weight: normal;
  }
  
  h1 {
    margin: 0;
    font-weight: bold;
    font-size: 1.4rem;
  }
  
  p {
    line-height: 1.4;
  }
  </style>