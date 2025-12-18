<script setup lang="ts"></script>
<template>
  <v-main>
    <v-app-bar>
      <v-app-bar-title>Application Bar</v-app-bar-title>

      <template v-slot:append>
        <v-btn color="grey" variant="tonal" icon="mdi-dots-vertical" />
      </template>
    </v-app-bar>

    <div>
      <slot />
    </div>
  </v-main>
</template>
