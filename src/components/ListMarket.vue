<template>
  <div class="table-responsive">
    <table class="table table-sm table-light align-items-center">
        <thead>
            <tr>
                <th scope="col" class="sort" data-sort="name">Currency</th>
                <th scope="col" class="sort" data-sort="budget">Last Price (IDR)</th>
                <th scope="col" class="sort" data-sort="status">24h Change</th>
            </tr>
        </thead>
        <tbody class="list">
          <tr v-for="item in markets" :key="item.id">
              <th scope="row">{{ item.cd }}</th>
              <td class="budget">{{ processCurrency(item.c) }}</td>
              <td :class="colorChange(item.cp)">{{ item.cp }}%</td>
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
    },
    colorChange (numb) {
      if (numb < 0) {
        return 'text-danger'
      } else {
        return 'text-success'
      }
    }
  }
}
</script>
