<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'

const API_KEY = "1B90548B36C0495886A01E6887F46860"
const API_URL = 'https://api.veriphone.io/v2/verify'
const MOBILE_NUMBER = ref('+2348024383756')
let mobileNumberInfo = ref(null)

const fetchMobileNumberInfo = async () => {
  try {
    const response = await axios.get(`${API_URL}?key=${API_KEY}&phone=${MOBILE_NUMBER.value}`)
    const mobileNumberInfo = response.data
    console.log(mobileNumberInfo)
  } catch (error) {
    console.log(error)
  }
}

onMounted(() => {
  fetchMobileNumberInfo()
})
</script>

<template>HELLO</template>
