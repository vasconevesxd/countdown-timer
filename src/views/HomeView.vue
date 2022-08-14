<template>
  <div class="container mx-auto">
    <Counter
      :year="year"
      :month="month"
      :currentDay="currentDay"
      :hour="hour"
      :minute="minute"
      :second="second"
      ref="counter"
    />
    <div class="container flex w-80 mx-auto mt-4">
      <DatePicker @date="selectedDate = $event" />
      <button
        :class="loaded ? btnClasses : btnClassesDisabled"
        @click="$refs.counter.showRemaining()"
        type="button"
        :disabled="!loaded"
      >
        Start
      </button>
    </div>
  </div>
</template>

<script>
import Counter from "@/components/Counter.vue";
import DatePicker from "@/components/Datepicker.vue";

export default {
  name: "HomeView",
  components: {
    Counter,
    DatePicker,
  },
  data() {
    return {
      selectedDate: null,
      year: null,
      month: null,
      currentDay: null,
      hour: null,
      minute: null,
      second: null,
      loaded: false,
      btnClasses:
        "shadow bg-purple-500 hover:bg-purple-400 focus:shadow-outline focus:outline-none  text-white font-bold py-2 px-4 rounded ml-4",
      btnClassesDisabled:
        "opacity-50 cursor-not-allowed shadow bg-purple-500 hover:bg-purple-400 focus:shadow-outline focus:outline-none  text-white font-bold py-2 px-4 rounded ml-4",
    };
  },
  watch: {
    selectedDate(newValue) {
      this.endDate(newValue);
    },
  },
  methods: {
    endDate(date) {
      if (date !== null) {
        this.year = date.getUTCFullYear();
        this.month = date.getUTCMonth();
        this.currentDay = date.getUTCDate();
        this.hour = date.getUTCHours();
        this.minute = date.getUTCMinutes();
        this.second = date.getUTCSeconds();
        this.loaded = true;
      }
    },
  },
};
</script>
