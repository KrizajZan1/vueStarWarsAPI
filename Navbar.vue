<!-- Created Navbar element which contains all the neccesary block like in figma -->
<template>
  <nav class="navbar">
    <ul>
      <li>Upcoming</li>
      <li>Legacy</li>
      <li id="logo">
        <img src="/images/Star_Wars_Logo.svg.png" alt="Star Wars logo" />
      </li>
      <li>Merch</li>
      <li>About</li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
};
</script>

<style scoped>
.navbar {
  width: 100%;
  height: 120px;
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
}

.navbar ul {
  list-style-type: none;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}

.navbar li {
  /* Change margin between elements so they appear more appart */
  margin: 0 50px;
  font-weight: bold;
  font-size: 18px;
}

#logo {
  height: 120px;
  /* Change margin around logo so elements are closer */
  margin: 0 20px;
  display: flex;
  justify-content: center;
}
</style>