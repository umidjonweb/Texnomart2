<template>
  <div class="clock">
    <div class="clock_inner">{{ hour.toString().padStart(2, "0") }}:</div>
    <div class="clock_inner">{{ minute.toString().padStart(2, "0") }}:</div>
    <div class="clock_inner">{{ second.toString().padStart(2, "0") }}</div>
  </div>
</template>

<script>
//  const hour = toString().padStart(2,'0');
//  const minute = toString().padStart(2,'0');
//  const second = toString().padStart(2,'0');

export default {
  name: "dasClock",
  props: {
    interval: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      hour: 0,
      minute: 20,
      second: 0,
    };
  },
  created() {
    setInterval(() => {
      if (this.second > 0 && this.second < 60) {
        this.second--;
      } else if (this.hour === 0 && this.minute === 0 && this.second === 0) {
        this.hour === 0;
        this.minute === 0;
        this.second === 0;
      } else {
        this.minute--;
        this.second = 59;
      }
    }, 1000);
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
.clock {
  display: flex;
  .clock_inner {
    font-size: 29px;
    font-weight: normal;
  }
}
</style>