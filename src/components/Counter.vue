<template>
  <div>
    {{ displayDays }}
    {{ displayHours }}
    {{ displayMinutes }}
    {{ displaySeconds }}
  </div>
</template>
<script>
export default {
  props: {},
  data() {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
    };
  },
  methods: {},
};
</script>
