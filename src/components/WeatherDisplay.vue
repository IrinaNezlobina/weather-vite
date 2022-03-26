<template>
  <div class="container">
    <table v-if="lang === 'ru'" class="table table-bordered">
      <thead></thead>
      <tbody>
        <tr>
          <th scope="row">Температура</th>
          <th scope="row">Закат</th>
          <th scope="row">Рассвет</th>
          <th scope="row">Минимальная температура</th>
        </tr>
        <tr>
          <td>{{ temp }}</td>
          <td>{{ new Date(sunset * 1000).getHours() }}:{{ new Date(sunset * 1000).getMinutes() }}</td>
          <td>{{ new Date(sunrise * 1000).getHours() }}:{{ new Date(sunrise * 1000).getMinutes() }}</td>
          <td>{{ tempMin }}</td>
        </tr>
        <tr>
          <th scope="row">Максимальная температура</th>
          <th scope="row">Скорость ветра</th>
          <th scope="row">Закат</th>
          <th scope="row">Минимальная температура</th>
        </tr>
        <tr>
          <td>{{ tempMax }} ℃</td>
          <td>{{ windSpeed }} м/сек</td>
          <td>{{ }}</td>
          <td>{{ }}</td>
        </tr>
      </tbody>
    </table>
    <table v-else class="table table-bordered">
      <thead></thead>
      <tbody>
        <tr>
          <th scope="row">Temperature</th>
          <th scope="row">Sunset</th>
          <th scope="row">Sunrise</th>
          <th scope="row">Min temperature</th>
        </tr>
        <tr>
          <td>{{ temp }} ℃</td>
          <td>{{ new Date(sunset * 1000).getHours() }}:{{ new Date(sunset * 1000).getMinutes() }}</td>
          <td>{{ new Date(sunrise * 1000).getHours() }}:{{ new Date(sunrise * 1000).getMinutes() }}</td>
          <td>{{ tempMin }}</td>
        </tr>
        <tr>
          <th scope="row">Max temperature </th>
          <th scope="row">Скорость ветра</th>
          <th scope="row">Закат</th>
          <th scope="row">Минимальная температура</th>
        </tr>
        <tr>
          <td>{{ tempMax }} ℃</td>
          <td>{{ windSpeed }} м/сек</td>
          <td>{{  }}</td>
          <td>{{ }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>


<script>
export default {
  props: {
    temp: { type: String, default: () => 0, required: false },
    sunset: { type: Number, default: () => 0, required: false },
    sunrise: { type: Number },
    tempMin: { type: Number },
    tempMax: { type: Number },
    windSpeed: { type: Number },
    lang: { type: String, required: false },
  },

  data() {
    return {

    }
  },
  updated() {
    // this.change(this.changeOption); //?
  }

}
</script>
<style>
.table {
  border: var(--main-color);
}
</style>