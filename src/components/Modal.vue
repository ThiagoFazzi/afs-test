<template>
  <div class="modal__overlay">
    <div class="modal__wrapper">
      <div class="modal__container">

        <div class="modal__header">
          <slot name="header"></slot>
        </div>

        <div class="modal__body">
          <slot name="body"></slot>
        </div>

        <div class="modal__footer">
          <slot name="footer" class="modal__footer--item"></slot>
          <button class="modal__footer--last-item" @click="$emit('close')">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'

@Component({ name: 'Modal' })
export default class Modal extends Vue {
  
}
</script>

<style scoped lang="scss">
@import '@/assets/styles/base.scss';
</style>