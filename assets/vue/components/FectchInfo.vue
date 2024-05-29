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

onMounted(() => {
  fetchMobileNumberInfo()
})
</script>

<template>
  <div v-if="mobileNumberInfo">
    <p>{{mobileNumberInfo.phone}}</p>
  </div>
</template>
