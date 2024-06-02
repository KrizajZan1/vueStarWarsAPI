<template>
  <div class="character-card" :style="{ backgroundImage: `url(${backgroundImage})` }">
    <div v-if="character" class="text">
      <p>Name: <b>{{ character.name }}</b></p>
      <p>Height: <b>{{ character.height }}</b></p>
      <p>Mass: <b>{{ character.mass }}</b></p>
      <p>Hair Color: <b>{{ character.hair_color }}</b></p>
      <p>Skin Color: <b>{{ character.skin_color }}</b></p>
      <p>Eye Color: <b>{{ character.eye_color }}</b></p>
      <p>Birth Year: <b>{{ character.birth_year }}</b></p>
      <p>Gender: <b>{{ character.gender }}</b></p>
      <button type="button" @click="$emit('edit')" class="edit-button">Edit</button>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CharacterCard",
  props: {
    character: Object,
    backgroundImage: String
  },
  mounted() {
    console.log("CharacterCard mounted with character:", this.character);
  }
};
</script>

<style scoped>
.character-card {
  border: 5px solid black;
  border-radius: 20px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  margin: 10px;
  width: 20%;
  height: 70%;
  overflow: hidden;
  box-shadow: 0 0 50px 10px rgba(255, 255, 0, 0.4);
}

.text {
  padding-top: 50%;
}

.edit-button {
  justify-content: center;
  align-items: center;
  width: 60%;
  font-size: 20px;
  background-color: yellow;
  border-radius: 10px;
}
</style>
