<template>
  <div class="slots">
    <div class="reels">
      <Reel ref="reelOne" />
      <Reel ref="reelTwo" />
      <Reel ref="reelThree" />
    </div>
    <div class="spacer"></div>
    <button @click="roll()">Roll</button>
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
    return {};
  },
  methods: {
    roll() {
      this.$refs.reelOne.spin(500, 500);
      this.$refs.reelTwo.spin(500, 500);
      this.$refs.reelThree.spin(500, 500);
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
