<script>
import axios from "axios";
import { store } from './store'

export default {
  data() {
    return {
      title: "Card VS Card",
      characters: [],
    };
  },


  methods: {
    fecthCharacters() {
      axios.get(`http://127.0.0.1:8000/api/characters`).then((res) => {
        // console.log(res.data.data);
        this.characters = res.data.data;
      });
    },

    random() {
      // for(let i = 1; i<=13; i++) {
        //prendo un id randomico
        // $randomId = rand(1, 13);
        const $randomId = Math.ceil(Math.random()*13)
        // this.characters.id = $randomId;
        console.log($randomId);
      // }

    }

  },

  mounted() {
    this.fecthCharacters();
  },
};
</script>

<template>
  <div class="container">
    <h1 class="text-center">{{ title }}</h1>
    
    <!-- BOTTONE -->
    <div class="text-center my-4">
      <button class="btn btn-success me-5" @click="random()">GIOCA TU!</button>
      <button class="btn btn-danger" @click="random()">GIOCA IL PC!</button>
    </div>

    <!-- CARD -->
    <div class="row g-3 mt-3">
      <div class="col-6" v-for="character in characters">
        <!-- <div class="card">
            <p><strong>ID: </strong>{{ character.id }}</p>
            <p><strong>Titolo: </strong>{{ character.name }}</p>
            <p><strong>Descrizione: </strong>{{ character.description }}</p>
            <p><strong>Forza: </strong>{{ character.strength }}</p>
            <p><strong>Difesa: </strong>{{ character.defence }}</p>
        </div> -->

        <div class="card h-100">
          <img :src="character.type.Image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ character.name }}</h5>
            <p class="card-text">
              {{ character.description }}
            </p>
          </div>
          <ul class="list-group list-group-flush">
            <li class="list-group-item">
              <strong>Attacco: </strong>{{ character.attack }}
            </li>
            <li class="list-group-item">
              <strong>Difesa: </strong>{{ character.defense }}
            </li>
            <li class="list-group-item">
              <strong>Velocità: </strong>{{ character.speed }}
            </li>
            <li class="list-group-item">
              <strong>Vita: </strong>{{ character.life }}
            </li>
          </ul>
          <div class="card-body">
            <a href="#" class="card-link">Card link</a>
            <a href="#" class="card-link">Another link</a>
          </div>
        </div>
      
      </div>
    </div>
  </div>
  
</template>

<style lang="scss">
  @import 'src/scss/general.scss';
</style>