<template>
  <div position: absolute>
    <v-card color="grey lighten-3" class="telemetry-tag">Telemetry</v-card>
    <v-card outlined class="telemetry-data">
      <v-text class="telemetry.data"> Сила тока: {{telemetry.amps}}A<br/></v-text>
      <v-text> Напряжение: {{telemetry.voltage}}V<br/></v-text>
      <v-text> Заряд батареи: {{telemetry.battery}}%<br/></v-text>
      <v-text> Крен: {{telemetry.roll}}°<br/></v-text>
      <v-text> Дифферент: {{telemetry.pitch}}°<br/></v-text>
      <v-text> Курс: {{telemetry.yaw}}°<br/></v-text>
      <v-text> Курс по gps: {{telemetry.gps_yaw}}°<br/></v-text>
      <v-text> Широта: {{telemetry.gps_lat}}°<br/></v-text>
      <v-text> Долгота: {{telemetry.gps_lng}}°<br/></v-text>
      <v-text> Высота над уровнем моря: {{telemetry.gps_alt}} м<br/></v-text>
      <v-text> Количество спутников: {{telemetry.gps_satellites}}<br/></v-text>
      <v-text> Скорость: {{telemetry.gps_speed}} м/с<br/></v-text>
    </v-card>
    <v-card color="grey lighten-3" class="status-tag">Status</v-card>
    <v-card outlined class="status-data">
      <v-text v-if="telemetry.mission"> Производится выполнение миссии <br/></v-text>
      <v-text v-else> В данный момент нет выполняемых миссий <br/></v-text>
      <v-text v-if="telemetry.charging">Аппарат заряжается<br/></v-text>
      <v-text v-else>Аппарат не заряжается<br/></v-text>
      <v-text v-if="telemetry.remote">Ручное управление<br/></v-text>
      <v-text v-else>Автономное управление<br/></v-text>
      <v-text v-if="telemetry.running">Аппарат выполняет движение<br/></v-text>
      <v-text v-else>Аппарат стоит на месте<br/></v-text>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'application',
  data () {
    return {
      telemetry: {
        amps: 0.0,
        battery: 0.0,
        charging: false,
        gps_alt: 0.0,
        gps_lat: 0.0,
        gps_lng: 0.0,
        gps_satellites: 0,
        gps_speed: 0.0,
        gps_yaw: 0.0,
        mission: false,
        pitch: 0.0,
        remote: false,
        roll: 0.0,
        running: false,
        voltage: 0.0,
        yaw: 0.0
      },
      remote_control: {
        axes: [0, 0, 0]
      }
    }
  },
  created: function () {
    this.ws = new WebSocket('ws://localhost:8081/ws')
    this.ws.onopen = function () {
      console.log('Connected')
    }
    this.ws.onclose = function (eventclose) {
      console.log('Connection closed, reason: ' + this.eventclose)
    }
    this.ws.onmessage = function (msg) {
      console.log('Message ' + this.msg)
    }
  }
}
</script>

<style scoped>
.v-card {
  width: 50%;
  left: 25%;
  max-width: 250px;
}
.v-simple-table {
  width: 50%;
  left: 0%;
}
.myFont {
  font-family: 'Arial Black', sans-serif;
}
.telemetry-data {
  transform: translate(150%, 5px);
  text-align: left;
}
.telemetry-tag {
  transform: translate(150%, 0);
}
.status-tag {
  transform: translate(150%, 10px);
}
.status-data {
  transform: translate(150%, 15px);
  text-align: left;
}
</style>
