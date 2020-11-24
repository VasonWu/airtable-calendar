<template>
  <div class="calendar-container">
    <full-calendar :events="events" locale="en"></full-calendar>
  </div>
</template>

<script>

var demoEvents = [
  {
    title: 'Sunny Out of Office',
    start: '2020-11-21',
    end: '2020-11-25'
  }
]

export default {
  name: 'HelloWorld',
  data () {
    return {
      fcEvents: demoEvents,
      events: []
    }
  },
  mounted () {
    let _this = this
    this.$axios
      .get('')
      .then(response => {
        response.data.records.forEach(item => {
          console.log(item)
          _this.events.push({
            title: item.fields.Name,
            start: item.fields.From,
            end: item.fields.To,
            cssClass: item.fields.Status
          })
        })
        console.log(_this.events)
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.calendar-container .full-calendar-body .dates .dates-events .events-week .events-day .event-box .event-item.Done {
  background-color: lightgray;
}
.calendar-container .full-calendar-body .dates .dates-events .events-week .events-day .event-box .event-item.Todo {
  background-color: lightgreen;
}
.calendar-container .full-calendar-body .dates .dates-events .events-week .events-day .event-box .event-item.InProcess {
  background-color: lightskyblue;
}
.calendar-container .full-calendar-body .dates .dates-events .events-week .events-day .event-box {
  height: 100px;
}
.calendar-container .comp-full-calendar {
  max-width: none;
}
.calendar-container .full-calendar-body .dates .week-row {
  height: 130px;
}
.calendar-container .full-calendar-body .dates .dates-events .events-week {
  height: 130px;
}
</style>
