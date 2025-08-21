<template>
  <div class="calendar-grid week-days">
    <div v-for="d in weekDays" :key="d" class="day-name">{{ d }}</div>
  </div>
</template>

<script lang="ts">
export default { name: 'CalendarWeekDays' }
</script>

<script setup lang="ts">
import { computed } from 'vue'

import dayjs from 'dayjs'

const props = defineProps<{ locale: string }>()

const weekDays = computed(() => {
  const start = dayjs().startOf('week')

  return Array.from({ length: 7 }).map((_, i) =>
    start.add(i, 'day').locale(props.locale).format('dd'),
  )
})
</script>

<style scoped>
.week-days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 4px;
}
.day-name {
  text-align: center;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
