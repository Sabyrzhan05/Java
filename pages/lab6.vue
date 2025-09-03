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
          Coordinates: {{ lake.lat }}, {{ lake.lng }}, Electrical Conductivity:{{ lake.level }}
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
  level:number
}

// Центр карты — Петропавловск
const petropavl = ref<LatLngTuple>([54.88, 69.16])

// Список озёр 
const lakes = ref<Lake[]>([
  { name: 'Озеро Пестрое', lat: 54.836699, lng: 69.111328, level: 1009 },
  { name: 'Озеро Белое', lat: 54.927154, lng: 69.254322, level: 1010 },
  { name: 'Озеро Поганка', lat: 54.920822, lng: 69.052810, level: 1013 },
  { name: 'Озеро Горькое', lat: 54.948165, lng: 68.950365, level: 1012},
  { name: 'Озеро Паганка', lat: 54.824701 , lng: 69.139179, level: 1015},
  { name: 'Озеро Дикое', lat: 54.839850 , lng: 69.131376, level: 1016},
  { name: 'Озеро Соленое', lat: 54.809068 , lng: 69.138382, level: 1045},
  { name: 'Озеро Большое Тинное', lat: 54.803751, lng:69.156091, level: 1012},
  { name: 'Озеро Гусиное', lat:54.792836, lng:69.137283, level: 1021 }, 
  { name: 'Озеро Пеньковское', lat:54.964895, lng:69.262492, level: 1051},
  
])
</script>