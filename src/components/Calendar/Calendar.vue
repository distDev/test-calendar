<template>
  <div class="calendar">
    <CalendarNav
      :current-date="currentDate"
      :locale="locale"
      @prev-month="prevMonth"
      @next-month="nextMonth"
    />

    <CalendarWeekDays :locale="locale" />

    <CalendarDays
      :current-date="currentDate"
      :selected-date="selectedDate"
      @select-date="selectDate"
    />

    <CalendarLocale v-model="locale" />
  </div>
</template>

<script lang="ts">
export default { name: 'Calendar' }
</script>

<script setup lang="ts">
import { ref } from 'vue'

import dayjs from 'dayjs'
import 'dayjs/locale/ru'
import 'dayjs/locale/en'

import type { Dayjs } from 'dayjs'

import CalendarNav from '@/components/Calendar/CalendarNav.vue'
import CalendarWeekDays from '@/components/Calendar/CalendarWeekDays.vue'
import CalendarLocale from '@/components/Calendar/CalendarLocale.vue'
import CalendarDays from '@/components/Calendar/CalendarDays.vue'

const emits = defineEmits<{
  (e: 'selectDate', day: string): void
}>()

const props = defineProps<{
  initialDate?: string
}>()

const locale = ref<'ru' | 'en'>('ru')

const baseDate: Dayjs = props.initialDate ? dayjs(props.initialDate, 'YYYY-MM-DD') : dayjs()

const currentDate = ref(baseDate)
const selectedDate = ref(baseDate)
const prevMonth = () => {
  currentDate.value = currentDate.value.subtract(1, 'month')
}

const nextMonth = () => {
  currentDate.value = currentDate.value.add(1, 'month')
}

const selectDate = (day: Dayjs) => {
  console.log(day)
  if (!day) return
  selectedDate.value = day

  const localeData = day.locale(locale.value).format('DD MMMM YY')
  emits('selectDate', localeData)
}
</script>

<style lang="scss" scoped>
.calendar {
  width: 280px;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 12px;
  font-family: sans-serif;
  user-select: none;
}
</style>
