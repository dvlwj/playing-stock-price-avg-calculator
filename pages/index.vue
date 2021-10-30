<template>
  <div class="container">
    <div>
      <h1 class="title">
        Calculator
      </h1>
      <van-row>
        <van-col>
          <h5 class='text-left'>Currently Owned</h5>
          <van-field v-model="bought" label="Shares Bought Price" placeholder="Shares Bought Price" />
          <van-field v-model="avg" label="AVG" readonly/>
          <van-field v-model="lot" label="Lot" placeholder="Lot" />
          <van-field v-model="totalBought" label="Total Bought" readonly/>
        </van-col>
        <van-col>
          <h5 class='text-left'>Buy</h5>
          <van-field v-model="runningPrice" label="Running Price" placeholder="Running Price" />
          <van-field disabled/>
          <van-field v-model="buyLot" label="Lot" placeholder="Lot" />
          <van-field v-model="runningTotal" label="Running Total"  readonly/>
        </van-col>
      </van-row>
      <van-field v-model="gainLoss" label="Percentage Gain/Loss"  readonly/>
      <van-field v-model="profitLoss" label="Total Profit/Loss"  readonly/>
      <van-field v-model="estimate" label="Estimated New Total Stocks AVG"  readonly/>
    </div>
  </div>
</template>

<script>
export default{
  data() {
    return {
      bought: null,
      avg: 0,
      lot: null,
      totalBought: 0,
      runningPrice: null,
      buyLot: null,
      runningTotal: 0,
      gainLoss: 0,
      profitLoss: 0,
      estimate: 0
    }
  },
  watch: {
    bought() {
      const lot = isNaN(this.lot) ? 0 : this.lot
      const bought = isNaN(this.bought) ? 0 : this.bought
      const runningPrice = isNaN(this.runningPrice) ? 0 : this.runningPrice
      const totalBought = (bought * lot * 100)
      const gainLoss = ((runningPrice - bought)/bought) * 100
      const profitLoss = (runningPrice - bought) * lot * 100
      this.profitLoss = isNaN(profitLoss) ? 0 : profitLoss
      this.gainLoss = isNaN(gainLoss) ? 0 : gainLoss
      this.totalBought = isNaN(totalBought) ? 0 : totalBought
    },
    totalBought() {
      const lot = isNaN(this.lot) ? 0 : this.lot
      const totalBought = isNaN(this.totalBought) ? 0 : this.totalBought
      const avg = (totalBought / lot / 100)
      const runningTotal = isNaN(this.runningTotal) ? 0 : this.runningTotal
      const buyLot = isNaN(this.buyLot) ? 0 : this.buyLot
      const estimated = ((totalBought + runningTotal) / (lot + buyLot)) / 100
      this.estimate = isNaN(estimated) ? 0 : estimated
      this.avg = isNaN(avg) ? 0 : avg
    },
    lot() {
      const totalBought = isNaN(this.totalBought) ? 0 : this.totalBought
      const lot = isNaN(this.lot) ? 0 : this.lot
      const buyLot = isNaN(this.buyLot) ? 0 : this.buyLot
      const avg = (totalBought / lot / 100)
      const bought = isNaN(this.bought) ? 0 : this.bought
      const runningPrice = isNaN(this.runningPrice) ? 0 : this.runningPrice
      const runningTotal = isNaN(this.runningTotal) ? 0 : this.runningTotal
      const profitLoss = (runningPrice - bought) * lot * 100
      const estimated = ((totalBought + runningTotal) / (lot + buyLot)) / 100
      this.estimate = isNaN(estimated) ? 0 : estimated
      this.profitLoss = isNaN(profitLoss) ? 0 : profitLoss
      this.avg = isNaN(avg) ? 0 : avg
    },
    runningPrice() {
      const buyLot = isNaN(this.buyLot) ? 0 : this.buyLot
      const lot = isNaN(this.lot) ? 0 : this.lot
      const runningPrice = isNaN(this.runningPrice) ? 0 : this.runningPrice
      const bought = isNaN(this.bought) ? 0 : this.bought
      const gainLoss = ((runningPrice - bought)/bought) * 100
      this.gainLoss = isNaN(gainLoss) ? 0 : gainLoss
      const profitLoss = (runningPrice - bought) * lot * 100
      this.profitLoss = isNaN(profitLoss) ? 0 : profitLoss
      const runningTotal = (runningPrice * buyLot * 100)
      this.runningTotal = isNaN(runningTotal) ? 0 : runningTotal
    },
    buyLot() {
      const totalBought = isNaN(this.totalBought) ? 0 : this.totalBought
      const buyLot = isNaN(this.buyLot) ? 0 : this.buyLot
      const lot = isNaN(this.lot) ? 0 : this.lot
      const runningPrice = isNaN(this.runningPrice) ? 0 : this.runningPrice
      const runningTotal = (runningPrice * buyLot * 100)
      const estimated = ((totalBought + runningTotal) / (lot + buyLot)) / 100
      this.estimate = isNaN(estimated) ? 0 : estimated
      this.runningTotal = isNaN(runningTotal) ? 0 : runningTotal
    },
    runningTotal() {
      const lot = isNaN(this.lot) ? 0 : this.lot
      const buyLot = isNaN(this.buyLot) ? 0 : this.buyLot
      const runningTotal = isNaN(this.runningTotal) ? 0 : this.runningTotal
      const totalBought = isNaN(this.totalBought) ? 0 : this.totalBought
      const estimated = ((totalBought + runningTotal) / (lot + buyLot)) / 100
      this.estimate = isNaN(estimated) ? 0 : estimated
    }
  },
  methods: {
    checkAvg: () => {
      return (this.totalBought / this.lot / 100)
    },
    checkTotalBought: () => {
      return (this.bought * this.lot * 100)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.text-left {
  text-align: left;
}
</style>
