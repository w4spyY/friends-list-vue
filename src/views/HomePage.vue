<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Els amics de Yuriy</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Els amics de Yuriy</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list>
       <CharacterListItem
         v-for="character in characters"
         :key="character.id"
         :character="character"
      />
     </ion-list>

      <ion-refresher slot="fixed" @ionRefresh="refresh($event)">
      <ion-refresher-content></ion-refresher-content>
     </ion-refresher> 

    </ion-content>

  </ion-page>
</template>

<script setup lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonList, IonRefresher, IonRefresherContent } from '@ionic/vue';
import CharacterListItem from '@/components/CharacterListItem.vue';
import { ref, onMounted } from 'vue';

interface Character {
  id: number;
  name: string;
  sate: string;
  image: string;
}

const characters = ref<Character[]>([]);
const fetchCharacters = async () => {
 try {
   const response = await fetch('https://rickandmortyapi.com/api/character');
   const data = await response.json();
   characters.value = data.results; // Asignamos los resultados a la lista
 } catch (error) {
   console.error('Error fetching characters:', error);
 }
};
onMounted(() => {
  fetchCharacters(); // Llamamos a la función al montar el componente
});
const refresh = (ev: CustomEvent) => {
 fetchCharacters().then(() => {
   ev.detail.complete(); // Finalizamos el refresher
 });
};


</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
