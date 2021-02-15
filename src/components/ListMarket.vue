<template>
  <div class="table-responsive d-flex justify-content-center align-items-center" style="min-height: 100vh;">
    <div v-if="loading">
      <img src='../assets/loading-45.gif' width='50px'/>
    </div>
    <table v-else class="table table-sm table-dark align-items-center mb-0">
        <thead>
            <tr>
                <th class="sort">Currency</th>
                <th class="sort">Last Price (IDR)</th>
                <th class="sort">24h Change</th>
            </tr>
        </thead>
        <tbody class="list">
          <tr v-for="item in markets" :key="item.id">
              <th scope="row"><a :href="'https://www.rekeningku.com/trade/'+ item.cd +'-IDR'" target="_blank" class="text-white">{{ item.cd }}</a></th>
              <td>{{ processCurrency(item.c) }}</td>
              <td :class="item.cp > 0 ? 'text-success' : 'text-danger'">{{ item.cp }}%</td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ListMarket',
  mounted () {
    axios
      .get('https://api.rekeningku.com/v2/price')
      .then(response => {
        this.markets = response.data
        this.loading = false
      })
  },
  data () {
    return {
      markets: null,
      loading: true
    }
  },
  methods: {
    processCurrency (curr) {
      return curr.toString().replace(/(\d)(?=(\d{3})+(?:\.\d+)?$)/g, '$1.')
    }
  }
}
</script>
