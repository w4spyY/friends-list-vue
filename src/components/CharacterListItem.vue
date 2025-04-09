<template>
    <ion-item v-if="character" :routerLink="'/character/' + character.id" :detail="false" class="list-item">
      <div slot="start">
        <img :src="character.image" alt="Character Image" class="character-image" />
      </div>
      <ion-label class="ion-text-wrap">
        <h2>{{ character.name }}</h2>
        <h3>Status: {{ character.status }}</h3>
    </ion-label>
 </ion-item>
</template>

<script setup lang="ts">
import { IonItem, IonLabel } from '@ionic/vue';

defineProps({
 character: Object,
});
</script>

<style scoped>
.character-image {
 width: 40px; /* Reduce el ancho */
 height: 40px; /* Reduce la altura */
 border-radius: 50%; /* Mantiene la imagen redonda */
 object-fit: cover; /* Asegura que la imagen se ajuste correctamente */
}

.list-item {
 --padding-start: 0;
 --inner-padding-end: 0;
 padding-left: 15px;
}

.list-item ion-label {
 margin-top: 12px;
 margin-bottom: 12px;
}

.list-item h2 {
 font-weight: 600;
 margin: 0;
  /**
  * With larger font scales
  * the date/time should wrap to the next
  * line. However, there should be
  * space between the name and the date/time
  * if they can appear on the same line.
  */
 display: flex;
 flex-wrap: wrap;
 justify-content: space-between;
}

.list-item p {
 text-overflow: ellipsis;
 overflow: hidden;
 white-space: nowrap;
 width: 95%;
}

.list-item .date {
 align-items: center;
 display: flex;
}

.list-item ion-icon {
 color: #c9c9ca;
}

.list-item ion-note {
 font-size: 0.9375rem;
 margin-right: 8px;
 font-weight: normal;
}

.list-item ion-note.md {
 margin-right: 14px;
}

.list-item .dot {
 display: block;
 height: 12px;
 width: 12px;
 border-radius: 50%;
 align-self: start;
 margin: 16px 10px 16px 16px;
}

.list-item .dot-unread {
 background: var(--ion-color-primary);
}
</style>