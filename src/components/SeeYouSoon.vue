<script setup lang="ts">
import { DateTime } from 'luxon'
import imgUrl from '../assets/we.jpeg'
const dateWhenWeWillMeetAgain = DateTime.fromObject(
  { day: 24, month: 5, hour: 8 },
  { zone: 'Europe/Athens' }
)
const dateNow = DateTime.fromObject({}, { zone: 'Europe/Athens' })
const diff = dateWhenWeWillMeetAgain.diff(dateNow, ['days', 'hours'])
const { days, hours } = diff.toObject()
</script>

<template>
  <div class="container">
    <p class="text">
      See you in {{ days }} days and {{ Math.floor(hours as number) }} hours, my love...
    </p>
    <img :src="imgUrl" />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4rem;
  padding: 0 1em;
}

.text {
  text-align: center;
}

img {
  width: 300px;
  aspect-ratio: 1;
  --_m: radial-gradient(#000 69%, #0000 70%) 84.5%/50%;
  -webkit-mask-box-image: var(--_m);
  mask-border: var(--_m);
  clip-path: polygon(-42% 0, 50% 91%, 142% 0);
  object-fit: cover;
}

@media (min-width: 1024px) {
  img {
    width: 400px;
  }
}

/* fallback until better support for mask-border */
@supports not (-webkit-mask-box-image: var(--_m)) {
  img {
    --_m: radial-gradient(at 70% 31%, var(--c) 29%, #0000 30%),
      radial-gradient(at 30% 31%, var(--c) 29%, #0000 30%),
      linear-gradient(#000 0 0) bottom/100% 50% no-repeat;
    -webkit-mask: var(--_m);
    mask: var(--_m);
  }
}
</style>
