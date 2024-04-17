<script>
import axios from "axios";
import { store } from './store'

export default {
  data() {
    return {
      title: "Card VS Card",
      characters: [],
      userCard: null,
      pcCard: null,
      userCardStrength: null,
      pcCardDefence: null,
      result: null
    };
  },

  methods: {
    fetchCharacters() {
      axios.get(`http://127.0.0.1:8000/api/characters`).then((res) => {
        this.characters = res.data.data;
      });
    },

    fetchCharacter(characterId, player) {
      axios.get(`http://127.0.0.1:8000/api/characters/${characterId}`)
        .then((res) =>{
          if (player === 'player') {
            this.userCard = res.data;
          } else {
            this.pcCard = res.data;
          }
        })
        .catch((err) =>{
          console.error(err)
        });
    },

    random() {
      const randomId = Math.ceil(Math.random()*this.characters.length)
      return randomId;
    },

    handleStart(player) {
      // il player può essere 'player' | 'pc'
      const randNum = this.random();
      this.fetchCharacter(randNum, player);
    },

    fight(){
      this.userCardStrength = this.userCard.strength;
      this.pcCardDefence = this.pcCard.defence;

      if( this.userCardStrength > this.pcCardDefence ){
        console.log(this.userCardStrength);
        console.log(this.pcCardDefence);
        alert("USER HA VINTO");
        
      } else if ( this.userCardStrength < this.pcCardDefence ) {
        console.log(this.userCardStrength);
        console.log(this.pcCardDefence);
        alert("PC HA VINTO");

      } else {
        console.log(this.userCardStrength);
        console.log(this.pcCardDefence);
        alert("PAREGGIO");
      }

    }
  },

  mounted() {
    this.fetchCharacters();
  },
};
</script>

<template>
  <div class="container">
    <h1 class="text-center">{{ title }}</h1>
    
    <!-- BOTTONE -->
    <div class="text-center my-4">
      <!-- <button  class="btn btn-success me-5" @click="random()">GIOCA TU!</button> -->
      <button class="btn btn-success me-5" @click="handleStart('player')">PESCA UNA CARTA!</button>
      <button class="btn btn-warning" @click="handleStart('pc')">PESCA LA CARTA DEL PC!</button>
    </div>

    <!-- CARD -->
    <div class="row g-3 mt-3">
      <div class="col-5 d-flex flex-column align-items-center">
        <h4>Card Giocatore</h4>
        <div v-if="userCard" class="card">
          <div class="card-header">
            <h5 class="card-title">{{ userCard.name }}</h5>
          </div>

          <div class="card-body">            
            <p class="card-text">
              {{ userCard.description }}
            </p>

            <ul class="list-group list-group-flush">
              <li class="list-group-item">
                <strong>Attacco: </strong>{{ userCard.strength }}
              </li>
              <li class="list-group-item">
                <strong>Difesa: </strong>{{ userCard.defence }}
              </li>
              <li class="list-group-item">
                <strong>Velocità: </strong>{{ userCard.speed }}
              </li>
              <li class="list-group-item">
                <strong>Vita: </strong>{{ userCard.life }}
              </li>
            </ul>
          </div>

          <!-- <div class="card-footer">
            <a href="#" class="card-link">Card link</a>
            <a href="#" class="card-link">Return link</a>
          </div> -->
        </div>

        <div v-else>
          <p>nessuna carta scelta</p>
        </div>
      </div>

      <div class="col-2 d-flex justify-content-center">
        <div>
          <button @click="fight()" class="text-center btn btn-danger">FIGHT!</button>
        </div>
      </div>

      <div class="col-5 d-flex flex-column align-items-center">
        <h4>Card Computer</h4>
        <div v-if="pcCard" class="card">
          <div class="card-header">
            <h5 class="card-title">{{ pcCard.name }}</h5>
          </div>

          <div class="card-body">            
            <p class="card-text">
              {{ pcCard.description }}
            </p>

            <ul class="list-group list-group-flush">
              <li class="list-group-item">
                <strong>Attacco: </strong>{{ pcCard.strength }}
              </li>
              <li class="list-group-item">
                <strong>Difesa: </strong>{{ pcCard.defence }}
              </li>
              <li class="list-group-item">
                <strong>Velocità: </strong>{{ pcCard.speed }}
              </li>
              <li class="list-group-item">
                <strong>Vita: </strong>{{ pcCard.life }}
              </li>
            </ul>
          </div>

          <!-- <div class="card-footer">
            <a href="#" class="card-link">Card link</a>
            <a href="#" class="card-link">Return link</a>
          </div> -->
        </div>

        <div v-else>
          <p>nessuna carta scelta</p>
        </div>
      </div>

      
    </div>
  </div>
</template>

<style lang="scss">
  @import 'src/scss/general.scss';
</style>