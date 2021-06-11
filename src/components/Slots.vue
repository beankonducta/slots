<template>
  <div class="slots">
    <div class="reels">
      <Reel ref="reelOne" :speed="25" @spun="spun(0, $event)" />
      <Reel ref="reelTwo" :speed="16" @spun="spun(1, $event)" />
      <Reel ref="reelThree" :speed="12" @spun="spun(2, $event)" />
    </div>
    <div class="spacer"></div>
    <div class="panel">
      <Lcd :title="'balance'" :value="balance" :type="'MONEY'" />
      <Lcd :title="'payout'" :value="payout" :type="'MONEY'" />
    </div>
    <div class="panel">
      <div class="sub-panel">
        <Lcd :title="'lines'" :value="lines" />
        <button class="change-btn" @click="multChange(-1)" :disabled="active || lines === 1">
          -
        </button>
        <button class="change-btn" @click="multChange(1)" :disabled="active || lines === 3">
          +
        </button>
      </div>
      <div class="sub-panel">
        <Lcd :title="'bet'" :value="bet" />
        <button class="change-btn" @click="betChange(-10)" :disabled="active || bet === 10">
          -
        </button>
        <button class="change-btn" @click="betChange(10)" :disabled="active || bet === 100">
          +
        </button>
      </div>
    </div>
    <button class="roll-btn" @click="roll()" :disabled="active || !canRoll">Roll</button>
  </div>
</template>

<script>
import Reel from "./Reel.vue";
import Lcd from "./Lcd.vue";

export default {
  name: "Slots",
  components: {
    Reel,
    Lcd,
  },
  props: {},
  data() {
    return {
      balance: 1000,
      bet: 10,
      lines: 1,
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
      this.$refs.reelOne.spin(300, 300);
      this.$refs.reelTwo.spin(300, 300);
      this.$refs.reelThree.spin(300, 300);
    },
    multChange(val) {
      if (val === 1 && this.lines < 3) this.lines += val;
      else if (val === -1 && this.lines > 1) this.lines += val;
    },
    betChange(val) {
      if (val === 10 && this.bet < 100) this.bet += val;
      else if (val === -10 && this.bet > 10) this.bet += val;
    },
    removeBet() {
      this.balance -= this.bet * this.lines;
    },
    spun(reel, value) {
      this.reels[reel].spun = true;
      this.reels[reel].values = value;
      for (let reel of this.reels) if (!reel.spun) return;
      this.active = false;
      this.payoutWinnings();
    },
    // TODO: Refactor
    payoutWinnings() {
      this.reels.forEach((val) => (val.spun = false));
      let payout = 0;
      for (let i = 0; i < this.reels.length - 1; i++)
        if (
          this.reels[0].values[i] === this.reels[1].values[i] &&
          this.reels[1].values[i] === this.reels[2].values[i]
        )
          if (i === 0 || this.lines > 1)
            payout += this.bet * this.lines * this.reels[0].values[i];
      if (
        this.reels[0].values[0] === this.reels[1].values[1] &&
        this.reels[1].values[1] === this.reels[2].values[2] &&
        this.lines >= 3
      )
        payout += this.bet * this.lines * this.reels[0].values[0];
      if (
        this.reels[0].values[2] === this.reels[1].values[1] &&
        this.reels[1].values[1] === this.reels[2].values[0] &&
        this.lines >= 3
      )
        payout += this.bet * this.lines * this.reels[0].values[2];
      this.payout = payout;
      this.balance += this.payout;
    },
  },
  computed: {
    canRoll() {
      return this.balance >= this.bet * this.lines;
    },
  },
};
</script>
<style scoped>
.slots {
  width: 100%;
}
.reels {
  width: 50%;
  display: flex;
  height: 40%;
  flex-direction: row;
  margin: 0 auto;
}

.panel {
  width: 50%;
  display: flex;
  flex-direction: row;
  flex-grow: 1;
  align-content: center;
  margin: 0 auto;
}

.sub-panel {
  width: 49.5%;
  padding-right: 1%;
}

.change-btn {
  width: 20%;
  margin: 5px;
  background: #0a0000;
  color: red;
}

.change-btn:hover:not(:disabled) {
  box-shadow: 0 0 10px 0 red inset, 0 0 20px 2px red;
}

button:disabled {
  border: 0px solid black;
  color: #274147;
  cursor: not-allowed;
}

.roll-btn {
  width: 50%;
  margin-top: 5%;
  color: black;
  background-color: #00d7c3;
}

.roll-btn:disabled {
  color: black;
  background-color: #294441;
}

.spacer {
  height: 50px;
}
</style>
