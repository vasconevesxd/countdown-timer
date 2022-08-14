<template>
  <section>
    <Datepicker v-model="date" :minDate="new Date()" />
  </section>
</template>

<script>
import Datepicker from "@vuepic/vue-datepicker";
import "@vuepic/vue-datepicker/dist/main.css";
export default {
  components: {
    Datepicker,
  },
  data() {
    return {
      date: null,
    };
  },
  watch: {
    date(newValue) {
      this.$emit("date", newValue);
    },
  },
};
</script>