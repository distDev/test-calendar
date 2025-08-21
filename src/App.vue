<template>
  <div class="calendar-container">
    <Calendar @selectDate="selectDate" :initial-date="customDate" />

    <div class="selected-date">
      <p>{{ selectedDate }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import Calendar from '@/components/Calendar/Calendar.vue'
import dayjs from 'dayjs'

const customDate = '2024-12-25'

const selectedDate = ref(dayjs(customDate).format('DD MMMM YY'))

const selectDate = (day: string) => {
  selectedDate.value = day
}
</script>

<style lang="scss" scoped>
.calendar-container {
  display: flex;
  align-items: flex-start;
  gap: 20px;

  @media (max-width: 650px) {
    flex-direction: column;
  }
}

.selected-date {
  padding: 5px 30px;
  border-radius: 12px;
  background: #e2eaf8;
}
</style>
