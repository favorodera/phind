<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'

const API_KEY = import.meta.env.VITE_VERIPHONE_API_KEY
const API_URL = 'https://api.veriphone.io/v2/verify'
const MOBILE_NUMBER = '+2348024383756'
const mobileNumberInfo = ref(null)

const fetchMobileNumberInfo = async () => {
  try {
    const response = await axios.get(`${API_URL}?key=${API_KEY}&phone=${MOBILE_NUMBER}`)
    mobileNumberInfo.value = response.data
    console.log(mobileNumberInfo)
  } catch (error) {
    console.log(error)
  }
}

// onMounted(() => {
//   fetchMobileNumberInfo()
// })
</script>

<template>
  <div class="main-container">
    <form method="get">
      <input type="tel" name="mobile-number" id="mobile-number" class="mobile-number" />
      <button type="submit" class="submit-button">CHECK</button>
    </form>

    <div class="info-container">
      <div v-if="mobileNumberInfo" class="info-is-generated">
        <div class="info">
          <p class="tittle">Country:</p>
          <p class="info-generated">{{ mobileNumberInfo.country }}</p>
        </div>
        <div class="info">
          <p class="tittle">Carrier:</p>
          <p class="info-generated">{{ mobileNumberInfo.carrier }}</p>
        </div>
        <div class="info">
          <p class="tittle">International Format:</p>
          <p class="info-generated">{{ mobileNumberInfo.international_number }}</p>
        </div>
        <div class="info">
          <p class="tittle">Local Format:</p>
          <p class="info-generated">{{ mobileNumberInfo.local_number }}</p>
        </div>
        <div class="info">
          <p class="tittle">Phone Region:</p>
          <p class="info-generated">{{ mobileNumberInfo.phone_region }}</p>
        </div>
        <div class="info">
          <p class="tittle">Phone Type:</p>
          <p class="info-generated">{{ mobileNumberInfo.phone_type }}</p>
        </div>
      </div>

      <div v-else class="info-is-not-generated">
        <div class="info-skeleton">
          <p class="tittle-skeleton"></p>
          <p class="info-generated-skeleton"></p>
        </div>
        <div class="info-skeleton">
          <p class="tittle-skeleton"></p>
          <p class="info-generated-skeleton"></p>
        </div>
        <div class="info-skeleton">
          <p class="tittle-skeleton"></p>
          <p class="info-generated-skeleton"></p>
        </div>
        <div class="info-skeleton">
          <p class="tittle-skeleton"></p>
          <p class="info-generated-skeleton"></p>
        </div>
        <div class="info-skeleton">
          <p class="tittle-skeleton"></p>
          <p class="info-generated-skeleton"></p>
        </div>
        <div class="info-skeleton">
          <p class="tittle-skeleton"></p>
          <p class="info-generated-skeleton"></p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main-container {
  width: 100%;
  max-width: 42rem;
  display: flex;
  flex-direction: column;
  background-color: #1c1c1c;
  align-items: center;
  padding: 2rem 0.5rem;
  justify-content: space-evenly;
  border-radius: 2rem;
  gap: 2rem;
}

form {
  width: 100%;
  display: flex;
  gap: 2%;
  justify-content: space-between;
  height: 2rem;
}

input {
  min-width: 10rem;
  background-color: #1c1c1c;
  border: 0.065rem solid #ffffff;
  border-radius: 0.5rem;
  flex-grow: 1;
  outline: none;
  padding: 1rem;
  text-align: center;
  font-size: 1.5rem;
  font-weight: 500;
}

button {
  max-width: 7rem;
  background-color: #1c1c1c;
  border: 0.065rem solid #ffffff;
  flex-grow: 1;
  border-radius: 0.5rem;
  cursor: pointer;
  outline: none;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
}
.info-container {
  width: 100%;
  display: flex;
}
.info-is-generated,
.info-is-not-generated {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.info, .info-skeleton {
  display: flex;
  width: 100%;
  justify-content: space-between;
}

.tittle {
  font-size: 1rem;
  font-weight: 600;
}

.info-generated {
  height: 1.5rem;
  font-weight: 500;
  text-transform: capitalize;
}

.tittle-skeleton {
  width: 60%;
  height: 1rem;
  background-color: #252525;
  border-radius: 5px;
  margin: 5px;
  animation: pulse 1.2s ease-in-out infinite;
}

.info-generated-skeleton {
  width: 40%;
  height: 1rem;
  background-color: #252525;
  border-radius: 5px;
  margin: 5px;
  animation: pulse 1.2s ease-in-out infinite;
}

@keyframes pulse {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.4;
  }
  100% {
    opacity: 1;
  }
}

</style>
