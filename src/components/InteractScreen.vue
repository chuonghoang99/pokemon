<template>
  <div class="interact_screen">
    <h1>Interact Component here</h1>
    <card-flip
      v-for="(card, index) in cardContext"
      :key="index"
      :ref="`card-${index}`"
      :prop_card="{ index: index, value: card }"
      @onFlip="checkFlip($event)"
    ></card-flip>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  props: {
    cardContext: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      rule: [],
    };
  },
  components: {
    CardFlip: Card,
  },
  methods: {
    checkFlip(card) {
      console.log(card);
      if (this.rule.length === 2) return false;
      this.rule.push(card);
      console.log(this.rule);

      if (this.rule.length === 2 && this.rule[0].value === this.rule[1].value) {
        console.log("right....");
        this.$refs[`card-${this.rule[0].index}`].isDisable = true;
        this.$refs[`card-${this.rule[1].index}`].isDisable = true;
        this.rule = [];
      } else if (
        this.rule.length === 2 &&
        this.rule[0].value != this.rule[1].value
      ) {
        console.log("wrong....");
        setTimeout(() => {
          this.$refs[`card-${this.rule[0].index}`].closeFlip();
          this.$refs[`card-${this.rule[1].index}`].closeFlip();
          this.rule = [];
        }, 500);
      }
    },
  },
};
</script>

<style></style>
