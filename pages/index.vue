<template>
  <div>
    <nav class="sticky top-0 bg-white font-bold text-2xl p-5 shadow">
      <h1>Impressions: {{ count }}</h1>
    </nav>
    <div class="w-full max-w-4xl p-5 mx-auto">
      <div
        v-for="(poem, idx) in poems"
        :key="idx"
        class="grid lg:grid-cols-12 gap-4 min-h-screen content-center"
      >
        <div class="lg:col-span-7">
          <observer @on-change="onChange">
            <img :src="poem.imageUrl" :alt="poem.imageAlt" class="w-full" />
          </observer>
        </div>
        <div class="lg:col-span-5">
          <p class="text-xl">{{ poem.text }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Observer from 'vue-intersection-observer'

export default {
  name: 'IndexPage',
  data() {
    return {
      count: 0,
      poems: [
        {
          text: `Low-anchored cloud, Newfoundland air, fountain head and source of rivers, dew-cloth, dream drapery, and napkin spread by fays; Drifting meadow of the air, where bloom the dasied banks and violets, and in whose fenny labyrinth the bittern booms and heron wades; Spirit of the lake and seas and rivers, bear only perfumes and the scent Of healing herbs to just men's fields! - Henry David Thoreau`,
          imageUrl: `https://res.cloudinary.com/dpkreativ/image/upload/v1646749176/wallpapers/mist.jpg`,
          imageAlt: `mist`,
        },
        {
          text: `Last night I drove a car, not knowing how to drive; not owning a car, I drove and knocked down people I loved...went 120 through one town. I stopped at Hedgeville and slept in the back seat... excited about my new life. - Gregory Corso`,
          imageUrl: `https://res.cloudinary.com/dpkreativ/image/upload/v1646483551/wallpapers/car.jpg`,
          imageAlt: `car`,
        },
        {
          text: `As your screen began to fade & flicker, and I shut you down & closed your cover, I knew all you needed was a little rest; I am so sorry for putting you to the test, but I cannot get through a day without you; You know how much I need you in all I do; You knew I would just die without your light; Good little laptop you gave me such a fright - Tia Maria`,
          imageUrl: `https://res.cloudinary.com/dpkreativ/image/upload/v1646695756/wallpapers/laptop.jpg`,
          imageAlt: `laptop`,
        },
      ],
    }
  },
  components: {
    Observer,
  },
  methods: {
    onChange(entry) {
      if (entry.isIntersecting) {
        this.count = this.count + 1
        localStorage.setItem('Impressions', this.count)
      }
    },
  },
}
</script>
