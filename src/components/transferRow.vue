<template>
  <div :class="`card theme-${colorName}`" :data-color="colorHex">
    <section class="card__shape">
      <div class="card__shape__side">
        <div class="card__shape__inner card__body">
          <div class="card__body__color-bar"></div>
          <h3 class="card__body__price">{{ transfer.amount }}</h3>
          <div class="card__body__divider"></div>
          <div class="card__body__transfer-path"></div>
          <div class="card__body__transfer-from-to">
            <p v-if="transfer.fromSecurityHolder">{{ transfer.fromSecurityHolder.fullName }}</p>
            <p v-else>None</p>
            <p v-if="transfer.toSecurityHolder">{{ transfer.toSecurityHolder.fullName }}</p>
            <p v-else>None</p>
          </div>
          <div class="card__body__date">
            Date
            <p>{{ transfer.recordDate }}</p>
          </div>
          <div class="card__body__footer card__body__footer--position">
            Position
            <p>{{ transfer.positionWithinDay }}</p>
          </div>
          <div class="card__body__footer card__body__footer--status">
            Status
            <p>{{ transfer.state }}</p>
          </div>
          <div class="card__body__footer card__body__footer--type">
            Type
            <p>{{ transfer.type }}</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";
import { Transaction } from "@/types/types";

@Component({
  name: "TransferRow",
})
export default class TransferRow extends Vue {
  @Prop({ required: true }) transfer!: Transaction;

  colorName = 'purple';
  colorHex = '#BA68C8';


}
</script>

<style lang="scss">
@import '@/assets/styles/base.scss';
</style>
