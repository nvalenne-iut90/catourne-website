<template>
  <div>
    <div class="main-container">
      <div class="container-options">
        <div>
          <div class="container-select">
            <label for="models">Modèles</label>
            <select id="models" v-model="model_selected" >
              <optgroup label="Modèles">
                <option value="capybara">Capybara</option>
                <option value="maxwell">Maxwell</option>
                <option value="floppa_cube">Floppa</option>
                <option value="el_gato">El Gato</option>
                <option value="gangnam_style">Gangnam Style</option>
                <option value="steve">Steve</option>
                <option value="shrek">Shrek</option>
              </optgroup>
            </select>
          </div>
          <div v-if="model_selected" class="container-select">
            <label for="musics">Musiques</label>
            <select id="musics" v-model="music_selected" @change="changeMusic(music_selected)">
              <optgroup label="Musiques">
                <option value="around_the_world">Around The World</option> <!-- c'est nous les daft punk -->
                <option value="ok_i_pull_up">Ok I Pull Up</option>
                <option value="you_spin_me_right_round">You spin me right round</option>
                <option value="maxwell_theme">Maxwell theme</option>
              </optgroup>
            </select>
          </div>
        </div>
        <div v-if="model_selected">
          <label for="check_party_mode" class="partyText">PARTY MODE</label>
          <input type="checkbox" id="check_party_mode" @click="party_mode()">
        </div>
      </div>
      <Renderer3D :modele="model_selected" v-if="model_selected" />
    </div>

    <div style="display: flex;justify-content: flex-end">
      <a href="https://marrantmaispastrop.fun/feur" target="_blank" style="text-decoration: none;color: black;">
        quoi
      </a>
    </div>
    <div style="position: fixed;bottom: 0; margin-bottom: 10px">by Nathan V.</div>
  </div>
</template>


<script>

import Renderer3D from "@/components/Renderer3D.vue";
let interval;
  export default {
    name: 'HomeView',

    components: {
      Renderer3D
    },
    data() {
      return {
        music_selected : '',
        model_selected : '',
        music_playing : null,
      }
    },
    methods : {
      stopMusic(){
        this.music_playing.pause();
      },
      changeMusic(music){
        if (this.music_playing)
          this.stopMusic();

        this.music_playing = new Audio(`./musics/${music}.mp3`)
        this.music_playing.play();
        this.music_playing.loop = true;
      },
      party_mode(){
          //this.is_party_mode = document.getElementById("check_party_mode").checked;
        if (document.getElementById("check_party_mode").checked){
          document.getElementById("musics").disabled = true;
          interval = setInterval(() => {
            document.documentElement.style.background = `rgb(${Math.random()*255},${Math.random()*255},${Math.random()*255})`
          }, 400)
          this.changeMusic("caramelldansen")

        } else {
          clearInterval(interval)
          document.getElementById("musics").disabled = false;
          if (this.music_selected) this.changeMusic(this.music_selected)
          else this.stopMusic()
          document.documentElement.style.background = "black"
        }
      }
    }
  }
</script>

<style scoped>
  .main-container, .container-options {
    display: flex;
    flex-flow: column wrap;
    align-items: center;
    justify-content: center;
  }

  .container-select{
    margin-bottom: 5px;
    display: flex;
    flex-flow: row wrap;
    align-items: center;
    justify-content: center;
  }
  #musics, #models {
    margin: 5px 10px 0 5px;
    background: black;
    color: white;
    height: 35px;
    font-size: 16px;
    border: white 2px solid;
    border-radius: 8px;
    width: 150px;
  }
  .partyText {
    animation-name: button_party_mode;
    animation-duration: 1s;
    animation-iteration-count: infinite;
  }
  #check_party_mode {
    width: 1.5em;
    height: 1.5em;
    border: 0.15em solid white;
    border-radius: 0.1em;
  }
  
  @media screen and (min-width: 460px) {
    #check_party_mode {
      width: 2em;
      height: 2em;
    }
    .partyText {
      font-size: 24px;
    }
  }

  @keyframes button_party_mode {
    0%   {color: green;}
    25%  {color: yellow;}
    50%  {color: blue;}
    100% {color: red;}
  }
</style>
