<template>
  <div class="container">
    <h1 class="title">Welcome to the best hello-world app</h1>
    <p class="label">Host Name</p>
    <p class="info">{{ hostName }}</p>
    <p class="label">Current Time</p>
    <p class="info">{{ currentTime }}</p>
    <p class="label">Your IP Address</p>
    <p class="info">{{ userIpAddress }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const hostName = ref('');
const currentTime = ref('');
const userIpAddress = ref('');

// Function to get the host name
const fetchHostName = () => {
  hostName.value = window.location.hostname;
};

// Function to update the current time
const updateTime = () => {
  const now = new Date();
  currentTime.value = now.toLocaleTimeString();
};

// Function to get the user's IP address
const fetchUserIpAddress = async () => {
  try {
    const response = await fetch('https://api64.ipify.org?format=json');
    const data = await response.json();
    userIpAddress.value = data.ip;
  } catch (error) {
    userIpAddress.value = 'Unable to fetch IP address';
  }
};

// Call the functions when the component is mounted
onMounted(async () => {
  fetchHostName();
  updateTime(); // Initial time update
  fetchUserIpAddress();
  setInterval(updateTime, 1000); // Update time every second
});
</script>

<style>
.container {
  font-family: 'Arial', sans-serif;
  text-align: center;
  background-color: #f5f5f5;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  max-width: 400px;
  margin: 0 auto;
}

.title {
  font-size: 28px;
  font-weight: 600;
  color: #007acc;
  margin: 10px 0;
}

.label {
  font-size: 18px;
  font-weight: 600;
  color: #333;
  margin-top: 15px;
}

.info {
  font-size: 20px;
  font-weight: 400;
  color: #333;
  margin-bottom: 15px;
}
</style>
