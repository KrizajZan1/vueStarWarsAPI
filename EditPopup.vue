<!-- Created form, which allows user to change data from Star Wars API -->
<template>
  <div class="popup">
    <div class="popup-content">
      <div>
        <h2>Editing character: {{ character.name }}</h2>
        <div v-if="character">
          <p>Name: <input v-model="character.name" placeholder="Change name" class="input"> </p>
          <p>Height: <input v-model="character.height" placeholder="Change height" class="input"> </p>
          <p>Mass: <input v-model="character.mass" placeholder="Change mass" class="input"> </p>
          <p>Hair Color: <input v-model="character.hair_color" placeholder="Change hair color" class="input"> </p>
          <p>Skin Color: <input v-model="character.skin_color" placeholder="Change skin color" class="input"> </p>
          <p>Eye Color: <input v-model="character.eye_color" placeholder="Change eye color" class="input"> </p>
          <p>Birth Year: <input v-model="character.birth_year" placeholder="Change birth year" class="input"> </p>
          <p>Gender: <input v-model="character.gender" placeholder="Change gender" class="input"> </p>
        </div>
        <button class="save" @click="savePopup"><b>Save</b></button>
        <button class="close" @click="closePopup"><b>Cancel</b></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["character"],
  methods: {
    savePopup() {
      this.$emit("save", this.character);
    },
    closePopup() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.popup-content {
  background-color: black;
  position: fixed;
  width: 30%;
  height: 50%;
  resize: none;
  padding: 20px;
  border-radius: 5px;
}

.input{
  float: right;
}

.save{
  background-color: green;
  margin-top: 20px;
  margin-right: 10px;
  width: 100px;
  height: 40px;
  font-size: 15px;
  border-radius: 7px;
}

.close{
  background-color: red;
  width: 100px;
  height: 40px;
  font-size: 15px;
  border-radius: 7px;
}
</style>