<template>
    <v-sheet
      class="d-flex align-content-end justify-center flex-wrap"
      style="background-color: rgb(32, 18, 18);"
    >
      <v-row justify="center">
        <v-col
          v-for="item in characters"
          :key="item.id"
          cols="12"
          sm="6"
          md="4"
          lg="3"
        >
          <v-card
            class="ma-4 pa-4"
            style="background-color: rgba(111, 0, 0, 0.766); border-radius: 5px;"
          >
            <v-img
              :src="`${item.thumbnail.path}/detail.${item.thumbnail.extension}`"
              height="400px"
              width="100%"
              cover
            ></v-img>
            <h2 style="color: rgb(255, 255, 255); 
            margin-bottom: 4%; 
            background-color: rgba(0, 0, 0, 0.565); 
            border-radius: 5px; 
            text-align: center; 
            border-color: rgb(0, 0, 0); border-style: double;" class="white--text">{{ item.name }}</h2>
            <v-btn
              color="red"
              @click="showDetails(item)"
              class="white--text">
              Ver mas
            </v-btn>
          </v-card>
        </v-col>
      </v-row>
  
      <v-dialog v-model="dialog" transition="dialog-bottom-transition">
        <v-card style="background-color: rgb(32, 18, 18);">
            <v-toolbar color="red" :title="selectedCharacter.name">
                <div style="background-color: red; border-radius: 5px; border-style: solid; border-color: black; margin-right: 1%;">
                    <v-btn color="black" @click="dialog = false">Cerrar</v-btn>
                </div>
            </v-toolbar>
          <div style="background-color: rgb(0, 0, 0); margin: 1%; border-radius: 5px; border-color: rgb(255, 255, 255); border-style: solid;">
            <center>
            <v-img
                :src="`${selectedCharacter.thumbnail.path}/detail.${selectedCharacter.thumbnail.extension}`"
                height="30%"
                width="30%"
                cover
                style="margin: 1%;"
            ></v-img>
            <h1 style="color: aliceblue;">{{ selectedCharacter.name }}</h1>
            </center>
          </div>
          <div style="background-color: rgba(111, 0, 0, 0.766); margin: 0.7%; border-radius: 5px; color: white; border-color: rgb(255, 255, 255); border-style: solid;">
          <h1 style="margin-left: 1%;">Description</h1>
          <v-card-text v-if="selectedCharacter.description !== ''">
            <p>{{ selectedCharacter.description }}</p>
          </v-card-text>
          <v-card-text v-else>
            <p>No se encontro descripcion para este personaje</p>
          </v-card-text>
          </div>
          <div style="background-color: rgba(111, 0, 0, 0.766); margin: 0.7%; border-radius: 5px; color: white; border-color: rgb(255, 255, 255); border-style: solid;">
          <h1 style="margin-left: 1%;">Comics</h1>
          <v-card-text>
            <p>{{ selectedCharacter.comics.available }}</p>
          </v-card-text>
          </div>
          <div style="background-color: rgba(111, 0, 0, 0.766); margin: 0.7%; border-radius: 5px; color: white; border-color: rgb(255, 255, 255); border-style: solid;">
          <h1 style="margin-left: 1%;">Series</h1>
          <v-card-text>
            <p>{{ selectedCharacter.series.available }}</p>
          </v-card-text>
          </div>
          <div style="background-color: rgba(111, 0, 0, 0.766); margin: 0.7%; border-radius: 5px; color: white; border-color: rgb(255, 255, 255); border-style: solid;">
          <h1 style="margin-left: 1%;">Stories</h1>
          <v-card-text>
            <p>{{ selectedCharacter.stories.available }}</p>
          </v-card-text>
          </div>
          <div style="background-color: rgba(111, 0, 0, 0.766); margin: 0.7%; border-radius: 5px; color: white; border-color: rgb(255, 255, 255); border-style: solid;">
          <h1 style="margin-left: 1%;">Events</h1>
          <v-card-text>
            <p>{{ selectedCharacter.events.available }}</p>
          </v-card-text>
          </div>
          <div style="background-color: rgba(111, 0, 0, 0.766); margin: 0.7%; border-radius: 5px; color: white; border-color: rgb(255, 255, 255); border-style: solid;">
          <h1 style="margin-left: 1%;">Outstanding Series</h1> 
          <v-card-text v-if="selectedCharacter.series.items.length > 0">
          <p v-for="(series, index) in selectedCharacter.series.items" :key="index" v-if="index < 3">
          {{ series.name }}
          </p>
          </v-card-text>
          <v-card-text v-else>
            <p>No hay Outstanding series para este personaje</p>
          </v-card-text>
          </div>
        </v-card>
      </v-dialog>
    </v-sheet>
  </template>
  
  <style>
    h1 {
      font-family: Verdana, Geneva, Tahoma, sans-serif;
    }
  
    h2 {
      font-family: Verdana, Geneva, Tahoma, sans-serif;
      font-size: 1.5rem;
      margin-top: 1rem;
    }
  
    p {
      font-weight: 500;
      font-family: Verdana, Geneva, Tahoma, sans-serif;
      font-size: 1rem;
      text-align: center;
    }
  </style>
  
  <script setup>
  import { ref } from "vue";
  import axios from "axios";
  
  const characters = ref([]);
  const dialog = ref(false);
  const selectedCharacter = ref(null);
  
  const loadCharacters = async () => {
    const url =
      "https://gateway.marvel.com/v1/public/characters?ts=1&apikey=064bf7f3a8d51ea6b15f4e755f0c78e6&hash=93f0f37ca0d13f65d78f0eea478d4fc0&limit=68";
    const { data } = await axios.get(url);
    characters.value = data.data.results;
  };
  
  const showDetails = (character) => {
    selectedCharacter.value = character;
    dialog.value = true;
  };
  
  loadCharacters();
  </script>
  