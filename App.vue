<template>
  <div id="app">
    <NavBar />
    <div id="container">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character.data"
        :background-image="character.image"
        @edit="editCharacter"
      />
    </div>
    <EditPopup v-if="isEditPopupVisible" :character="selectedCharacter" @close="closeEditPopup" />
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
      selectedCharacter: null
    };
  },
  async mounted() {
    await Promise.all(
      this.characters.map(async (character) => {
        try {
          const response = await axios.get(character.url);
          character.data = response.data;
          console.log(
            `Fetched data for character ${character.id}:`,
            character.data
          );
        } catch (error) {
          console.error(`Error fetching data for ${character.id}:`, error);
        }
      })
    );
  },
  methods: {
    editCharacter(characterData) {
    this.selectedCharacter = characterData;
    this.isEditPopupVisible = true;
  },

    closeEditPopup() {
      this.isEditPopupVisible = false;
    }
  }
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
  height: 100vh;
}
</style>
