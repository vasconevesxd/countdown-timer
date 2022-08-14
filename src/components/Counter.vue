<template>
  <section v-if="loaded" class="flex items-baseline justify-center mt-14">
    <div class="flex flex-col items-center">
      <p class="text-6xl">{{ displayDays }}</p>
      <p>days</p>
    </div>
    <span class="mx-2 text-6xl">:</span>
    <div class="flex flex-col items-center">
      <p class="text-6xl">{{ displayHours }}</p>
      <p>hours</p>
    </div>
    <span class="mx-2 text-6xl">:</span>
    <div class="flex flex-col items-center">
      <p class="text-6xl">{{ displayMinutes }}</p>
      <p>minutes</p>
    </div>
    <span class="mx-2 text-6xl">:</span>
    <div class="flex flex-col items-center">
      <p class="text-6xl">{{ displaySeconds }}</p>
      <p>seconds</p>
    </div>
  </section>
  <section class="flex items-baseline justify-center mt-14" v-else>
    <div class="flex flex-col items-center">
      <p class="text-6xl">00</p>
      <p>days</p>
    </div>
    <span class="mx-2 text-6xl">:</span>
    <div class="flex flex-col items-center">
      <p class="text-6xl">00</p>
      <p>hours</p>
    </div>
    <span class="mx-2 text-6xl">:</span>
    <div class="flex flex-col items-center">
      <p class="text-6xl">00</p>
      <p>minutes</p>
    </div>
    <span class="mx-2 text-6xl">:</span>
    <div class="flex flex-col items-center">
      <p class="text-6xl">00</p>
      <p>seconds</p>
    </div>
  </section>
</template>
<script>
export default {
  props: ["year", "month", "currentDay", "hour", "minute", "second"],
  data() {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      loaded: false,
    };
  },
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60;
    },
    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
    end() {
      return new Date(
        this.year,
        this.month,
        this.currentDay,
        this.hour,
        this.minute,
        this.second
      );
    },
  },
  methods: {
    formaNum: (num) => (num < 10 ? "0" + num : num),
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();

        const distance = this.end.getTime() - now.getTime();
        if (distance < 0) {
          clearInterval(timer);
          return;
        }
        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.displayDays = this.formaNum(days);
        this.displayHours = this.formaNum(hours);
        this.displayMinutes = this.formaNum(minutes);
        this.displaySeconds = this.formaNum(seconds);
        this.loaded = true;
      }, 1000);
    },
  },
};
</script>
