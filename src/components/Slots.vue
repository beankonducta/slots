<template>
  <div class="slots">
    <div class="reels">
      <Reel ref="reelOne" @spun="spun(0, $event)" />
      <Reel ref="reelTwo" @spun="spun(1, $event)" />
      <Reel ref="reelThree" @spun="spun(2, $event)" />
    </div>
    <div class="spacer"></div>
    <button @click="roll()" :disabled="active">Roll</button>
    bal: {{ balance }}
    pay: {{ payout }}
  </div>
</template>

<script>
import Reel from "./Reel.vue";

export default {
  name: "Slots",
  components: {
    Reel,
  },
  props: {},
  data() {
    return {
      balance: 1000,
      bet: 10,
      multiplier: 1,
      payout: 0,
      reels: [
        { spun: false, values: [0, 0, 0] },
        { spun: false, values: [0, 0, 0] },
        { spun: false, values: [0, 0, 0] },
      ],
      active: false,
    };
  },
  methods: {
    roll() {
      this.active = true;
      this.payout = 0;
      this.removeBet();
      this.$refs.reelOne.spin(500, 500);
      this.$refs.reelTwo.spin(500, 500);
      this.$refs.reelThree.spin(500, 500);
    },
    removeBet() {
      this.balance -= this.bet * this.multiplier;
    },
    spun(reel, value) {
      this.reels[reel].spun = true;
      this.reels[reel].values = value;
      for (let reel of this.reels) if (!reel.spun) return;
      this.active = false;
      this.payoutWinnings();
    },
    payoutWinnings() {
      if (
        this.reels[0].values[1] === this.reels[1].values[1] &&
        this.reels[1].values[1] === this.reels[2].values[1]
      ) {
        this.payout = this.bet * this.multiplier * this.reels[0].values[1];
        this.balance += this.payout;
      }
    },
  },
  computed: {
    canRoll() {
      return this.balance >= this.bet * this.multiplier;
    },
  },
};
</script>
<style scoped>
.slots {
  width: 100%;
}
.reels {
  width: 25%;
  display: flex;
  flex-direction: row;
  margin: 0 auto;
}
.spacer {
  height: 200px;
}
</style>
