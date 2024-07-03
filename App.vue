<template>
  <div id="app">
    <NavBar />
    <div id="container">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character.data"
        :background-image="character.image"
        @edit="editCharacter(character)"
      />
    </div>
    <EditPopup v-if="isEditPopupVisible" :character="selectedCharacter" @close="closeEditPopup" @save="updateCharacter"/>
  </div>
</template>

<script>
import NavBar from "./Navbar.vue";
import CharacterCard from "./CharacterCard.vue";
import axios from "axios";
import EditPopup from "./EditPopup.vue";

import yodaImage from "../images/yoda.jpg";
import darthVaderImage from "../images/darthVader.jpg";
import obiWanKenobiImage from "../images/obiWanKenobi.webp";

export default {
  name: "App",
  components: {
    NavBar,
    CharacterCard,
    EditPopup,
  },
  data() {
    return {
      characters: [
        {
          id: 1,
          url: "https://swapi.dev/api/people/20/",
          image: yodaImage,
          data: null,
        },
        {
          id: 2,
          url: "https://swapi.dev/api/people/4/",
          image: darthVaderImage,
          data: null,
        },
        {
          id: 3,
          url: "https://swapi.dev/api/people/10/",
          image: obiWanKenobiImage,
          data: null,
        },
      ],
      isEditPopupVisible: false,
      selectedCharacter: null,
    };
  },
  // -----------------------------------------------------------------------------------------------------------------------------------
  async mounted() {
    this.characters = await Promise.all(
      this.characters.map(async (character) => {
        const localCharacterData = localStorage.getItem(`character_${character.id}`);
        if (localCharacterData) {
          character.data = JSON.parse(localCharacterData);
        } else {
          try {
            const response = await axios.get(character.url);
            character.data = response.data;
            localStorage.setItem(`character_${character.id}`, JSON.stringify(character.data));
          } catch (error) {
            console.error(`Error fetching data for ${character.id}:`, error);
          }
        }
        return character;
      })
    );
  // ----------------------------------------------------------------------------------------------------------------------------------- 
    console.log(localStorage);
  },
  methods: {
    editCharacter(character) {
      this.selectedCharacter = character.data;
      this.isEditPopupVisible = true;
    },
    closeEditPopup() {
      this.isEditPopupVisible = false;
    },
    // --------
    updateCharacter(updatedCharacter) {
      const index = this.characters.findIndex((character) => character.data.url === updatedCharacter.url);
      if (index !== -1) {
        this.characters[index].data = updatedCharacter;
        localStorage.setItem(`character_${this.characters[index].id}`, JSON.stringify(updatedCharacter));
      }
      this.closeEditPopup();
    // --------
    },
  },
};
</script>

<style>
body {
  background-color: black;
  color: white;
  margin: 0;
}

#container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
</style>
