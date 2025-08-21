<template>
  <div class="calendar-days">
    <div
      v-for="(day, index) in daysList"
      :key="index"
      class="day"
      :class="{
        selected: isSelected(day),
        'other-month': day.month() !== currentDate.month(),
      }"
      @click="selectDate(day)"
    >
      {{ day.date() }}
    </div>
  </div>
</template>

<script lang="ts">
export default { name: 'CalendarDays' }
</script>

<script setup lang="ts">
import { computed } from 'vue'
import type { Dayjs } from 'dayjs'

const emits = defineEmits<{
  (e: 'selectDate', day: Dayjs): void
}>()

const props = defineProps<{
  currentDate: Dayjs
  selectedDate: Dayjs
}>()

const daysList = computed<Dayjs[]>(() => {
  const startOfMonth = props.currentDate.startOf('month')
  const endOfMonth = props.currentDate.endOf('month')

  const start = startOfMonth.startOf('week')
  const end = endOfMonth.endOf('week')

  const days: Dayjs[] = []
  let day = start

  while (day.isBefore(end) || day.isSame(end, 'day')) {
    days.push(day)
    day = day.add(1, 'day')
  }

  return days
})

const isSelected = (day: Dayjs): boolean => {
  if (!day) return false
  return day.isSame(props.selectedDate, 'day')
}

const selectDate = (day: Dayjs) => {
  emits('selectDate', day)
}
</script>

<style lang="scss" scoped>
.calendar-days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 4px;
}

.day {
  text-align: center;
  padding: 6px 0;
  cursor: pointer;
  border-radius: 4px;
  color: #091a48;

  &.selected {
    box-shadow: 0 0 0 2px #007bff inset;
    border-radius: 4px;
    font-weight: bold;
  }

  &.other-month {
    opacity: 30%;
  }

  &:hover {
    background: #e2eaf8;
  }
}
</style>
