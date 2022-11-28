<script setup>
import { ref } from "vue";

const userInfo = ref([]);

async function getUser() {
  const results = await fetch("https://randomuser.me/api");
  const finalRes = await results.json();
  userInfo.value = finalRes.results[0];

  console.log(fullAddress);
}

getUser();
</script>

<template>
  <div class="container">
    <div :class="userInfo.gender === 'female' ? 'female' : 'male'">
      <img :src="userInfo.picture.large" />
    </div>
    <div class="info">
      <h2>{{ userInfo.name.first }} {{ userInfo.name.last }}</h2>
      <h3>Age: {{ userInfo.dob.age }}</h3>
      <h4>
        Address: {{ userInfo.location.street.number }}
        {{ userInfo.location.street.name }}, {{ userInfo.location.city }},
        {{ userInfo.location.state }} {{ userInfo.location.postcode }}
      </h4>
      <h4>Email: {{ userInfo.email }}</h4>
    </div>
    <button
      :class="userInfo.gender === 'female' ? 'female-button' : 'male-button'"
      @click="getUser"
    >
      Get Random User
    </button>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  height: 600px;
  margin: 100px auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.female img {
  height: 200px;
  width: 200px;
  border-radius: 50%;
  border: pink 8px solid;
}

.male img {
  height: 200px;
  width: 200px;
  border-radius: 50%;
  border: blue 8px solid;
}

.female-button {
  background-color: pink;
  color: black;
  padding: 10px;
  border-radius: 45px;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
  cursor: pointer;
}

.male-button {
  background-color: blue;
  color: white;
  padding: 10px;
  border-radius: 45px;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
  cursor: pointer;
}

.info {
  text-align: center;
}
</style>
