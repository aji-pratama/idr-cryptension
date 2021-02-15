<template>
  <div class="table-responsive">
    <table class="table table-sm table-dark align-items-center mb-0">
        <thead>
            <tr>
                <th scope="col" class="sort" data-sort="name">Currency</th>
                <th scope="col" class="sort" data-sort="budget">Last Price (IDR)</th>
                <th scope="col" class="sort" data-sort="status">24h Change</th>
            </tr>
        </thead>
        <tbody class="list">
          <tr v-for="item in markets" :key="item.id">
              <th scope="row"><a :href="'https://www.rekeningku.com/trade/'+ item.cd +'-IDR'" target="_blank" class="text-white">{{ item.cd }}</a></th>
              <td class="budget">{{ processCurrency(item.c) }}</td>
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
      .then(response => (this.markets = response.data))
  },
  data () {
    return {
      markets: null
    }
  },
  methods: {
    processCurrency (curr) {
      return curr.toString().replace(/(\d)(?=(\d{3})+(?:\.\d+)?$)/g, '$1.')
    }
  }
}
</script>
