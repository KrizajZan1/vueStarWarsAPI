<!-- Created form, which allows user to change data from Star Wars API -->
<template>
  <div class="popup">
    <div class="popup-content">
      <div v-if="id = 1">
        <h2>Editing character: {{ character.name }}</h2>
        <div v-if="character">
          <p>Name: <b>{{ character.name }}</b></p>
          <input v-model="newname" placeholder="Change name"> 
          <p>Height: <b>{{ character.height }}</b></p>
          <p>Mass: <b>{{ character.mass }}</b></p>
          <p>Hair Color: <b>{{ character.hair_color }}</b></p>
          <p>Skin Color: <b>{{ character.skin_color }}</b></p>
          <p>Eye Color: <b>{{ character.eye_color }}</b></p>
          <p>Birth Year: <b>{{ character.birth_year }}</b></p>
          <p>Gender: <b>{{ character.gender }}</b></p>
        </div>
        <button class="save" @click="savePopup">Save</button>
        <button class="close" @click="closePopup">Cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["character"],
  methods: {
    savePopup() {
      localStorage.setItem('newname', this.newname),
      console.log(localStorage), // --------------------------------------------
      this.closePopup();
    },
    closePopup() {
      this.$emit("close");
    }
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
  padding: 20px;
  border-radius: 5px;
}

.save{
  margin-top: 20px;
  margin-right: 10px;
}
</style>