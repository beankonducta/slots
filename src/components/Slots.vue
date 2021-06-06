<template>
  <div class="slots">
    <Reel ref="reelOne" />
    <Reel ref="reelTwo" />
    <Reel ref="reelThree" />
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
    }
  },
};
</script>
<style scoped>
.slots {
  width: 100%;
}
</style>
