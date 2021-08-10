<template>
  <div class="about pa-3">
    <v-container class="mt-12">
      <v-row class="mt-6" justify="center">
        <v-date-picker v-model="selectDate" color="green" locale="en"></v-date-picker>
        <v-col cols=12>
          <div>{{ selectDate }}</div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
