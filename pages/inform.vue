<template>
  <div style="height:100vh; width:100vw">
    <LMap
      :zoom="11"
      :center="petropavl"
      :use-global-leaflet="false"
      style="height:100%; width:100%;"
    >
      <LTileLayer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&copy; OpenStreetMap contributors"
      />

      <!-- Маркер города -->
      <LMarker :lat-lng="petropavl" :draggable="false">
        <LTooltip permanent direction="top">Петропавловск (СКО)</LTooltip>
        <LPopup>Петропавловск, Северо-Казахстанская область</LPopup>
      </LMarker>

      <!-- Зафиксированные озёра -->
      <LMarker
        v-for="(lake, i) in lakes"
        :key="i"
        :lat-lng="[lake.lat, lake.lng]"
        :draggable="false"
      >
        <LTooltip permanent direction="top">{{ lake.name }}</LTooltip>
        <LPopup>
          <strong>{{ lake.name }}</strong><br />
          Coordinates: {{ lake.lat }}, {{ lake.lng }}, Patogens: {{ lake.patogens }}
        </LPopup>
      </LMarker>
    </LMap>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { LMap, LTileLayer, LMarker, LTooltip, LPopup } from '@vue-leaflet/vue-leaflet'
import 'leaflet/dist/leaflet.css'

type LatLngTuple = [number, number]

interface Lake {
  name: string
  lat: number
  lng: number
  patogens: string
}

// Центр карты — Петропавловск
const petropavl = ref<LatLngTuple>([54.88, 69.16])

// Список озёр 
const lakes = ref<Lake[]>([
  { name: 'Озеро Пестрое', lat: 54.836699, lng: 69.111328, patogens: "Отсутсвует" },
  { name: 'Озеро Белое', lat: 54.927154, lng: 69.254322,patogens: "Есть небольшой риск" },
  { name: 'Озеро Поганка', lat: 54.920822, lng: 69.052810,patogens: "Присутствует" },
  { name: 'Озеро Горькое', lat: 54.948165, lng: 68.950365,patogens: "Есть небольшой риск"},
  { name: 'Озеро Паганка', lat: 54.824701 , lng: 69.139179,patogens: "Присутствует"},
  { name: 'Озеро Дикое', lat: 54.839850 , lng: 69.131376,patogens: "Отсутсвует"},
  { name: 'Озеро Соленое', lat: 54.809068 , lng: 69.138382,patogens: "Отсутсвует"},
  { name: 'Озеро Большое Тинное', lat: 54.803751, lng:69.156091,patogens: "Есть небольшой риск"},
  { name: 'Озеро Гусиное', lat:54.792836, lng:69.137283,patogens: "Есть небольшой риск" }, 
  { name: 'Озеро Пеньковское', lat:54.964895, lng:69.262492,patogens: "Отсутсвует"},
  
])
</script>