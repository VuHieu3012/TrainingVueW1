<template>
  <div style="background-color: #ececec; padding: 20px">
    <a-row :gutter="20">
      <a-col :span="8">
        <a-card title="Days" :bordered="false" style="width: 150px">
          <p>{{ displayDays }}</p>
        </a-card>
      </a-col>
      <a-col :span="8">
        <a-card title="Hours" :bordered="false" style="width: 150px">
          <p>{{ displayHours }}</p>
        </a-card>
      </a-col>
      <a-col :span="8">
        <a-card title="Minutes" :bordered="false" style="width: 150px">
          <p>{{ displayMinutes }}</p>
        </a-card>
      </a-col>
      <a-col :span="8">
        <a-card title="Second" :bordered="false" style="width: 150px">
          <p>{{ displaySeconds }}</p>
        </a-card>
      </a-col>
    </a-row>
  </div>
</template>

<script>
export default {
  data: () => ({
    displayDays: 0,
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0,
  }),

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
  },

  mounted() {
    this.showRemaining();
  },

  methods: {
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();
        const end = new Date(2020, 4, 10, 10, 10, 10);
        const distance = end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          return;
        }

        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.displayMinutes = minutes < 10 ? "0" + minutes : minutes;
        this.displaySeconds = seconds < 10 ? "0" + seconds : seconds;
        this.displayHours = hours < 10 ? "0" + hours : hours;
        this.displayDays = days < 10 ? "0" + days : days;
      }, 1000);
    },
  },
};
</script>

<style lang="css" scoped>
:where(.css-dev-only-do-not-override-185kyl0).ant-col-8 {
  display: block;
  flex: 25%;
  max-width: 25%;
}
.ant-card-body {
  font-size: 24px;
}
</style>
