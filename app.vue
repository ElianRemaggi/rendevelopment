<script setup>
//saturate-150 contrast-100'
</script>

<template>
  <!-- Contenedor principal (cubre toda la pantalla) -->
  <div class="relative min-h-screen font-mono ">
    <!-- Capa del fondo con filtros -->
    <div 
      class="fixed inset-0 -z-10 bg-[url('@/assets/cover.png')] bg-cover bg-center filter hue-rotate-1 ">
    </div>

    <!-- Capa del contenido (sin filtros) -->
    <div class="relative">
      <NuxtRouteAnnouncer />
      <NuxtPage />
    </div>
  </div>
</template>