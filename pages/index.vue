<template>
  <div class="pa3 ph5-l">
    <h1>
      Nuxt.js Advent Calendar 2019
    </h1>

    <p class="mb4 lh-copy">{{ comment }}</p>

    <div class="flex flex-wrap ba b--black-10">
      <div
        v-for="dayName in dayNames"
        :key="dayName"
        class="calendar-item f4 bg-near-black white mv0 pv2 ph3"
      >
        {{ dayName }}
      </div>

      <article
        v-for="day in days"
        :key="day.date"
        class="calendar-item ba b--black-10"
      >
        <p class="f4 bg-near-white black-60 mv0 pv2 ph3">
          {{ day.date }}
        </p>

        <div class="pa3 tc">
          <img
            :src="day.authorImageUrl"
            :alt="day.authorName"
            class="br-100 h3 w3 dib"
          >

          <a
            :href="`https://qiita.com/${day.authorName}`"
            target="_blank"
            rel="noopener noreferrer"
            class="db link hover-blue lh-copy measure center f6 black-70"
          >
            {{ day.authorName }}
          </a>

          <hr class="mw3 mv3 bb bw1 b--black-10 center">

          <a v-if="day.articleUrl !== null"
            :href="day.articleUrl"
            target="_blank"
            rel="noopener noreferrer"
            class="db blue link f6 f5-ns lh-copy measure tl dim"
          >
            {{ day.comment }}
          </a>

          <p v-else
            class="f6 f5-ns lh-copy measure tl"
          >
            {{ day.comment }}
          </p>
        </div>
      </article>

      <div
        v-for="dayName in [26, 27, 28]"
        :key="dayName"
        class="calendar-item ba b--black-10"
      >
        <p class="f4 bg-near-white black-60 mv0 pv2 ph3">
          {{ dayName }}
        </p>
      </div>
    </div>

    <p class="mv4 lh-copy">
      ※ このページはレスポンシブ対応していません。デスクトップサイズの画面でご覧ください。
    </p>
  </div>
</template>

<script>
import { parse } from 'node-html-parser'

export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get('https://qiita.com/advent-calendar/2019/nuxt-js')
    const root = parse(data)
    return {
      comment: root.querySelector('.markdownContent').text,
      dayNames: root.querySelectorAll('.adventCalendarCalendar_dayName').map(dayName => dayName.text),
      days: root.querySelectorAll('.adventCalendarCalendar_day').map(day => {
        const articleUrl = day.querySelector('.adventCalendarCalendar_comment').querySelector('a') ?
          day.querySelector('.adventCalendarCalendar_comment').querySelector('a').attributes['href'] :
          null
        return {
          date: day.querySelector('.adventCalendarCalendar_date').text,
          authorName: day.querySelector('.adventCalendarCalendar_author').text.replace(/\s|&nbsp;/g, ''),
          authorImageUrl: day.querySelector('.adventCalendarCalendar_authorIcon').attributes['src'],
          comment: day.querySelector('.adventCalendarCalendar_comment').text,
          articleUrl: articleUrl
        }
      })
    }
  }
}
</script>

<style>
.calendar-item {
  width: calc(100% / 7);
}
</style>
