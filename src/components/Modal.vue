<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-mask__wrapper">
        <div class="modal-mask__container">

          <div class="modal-mask__header">
            <slot name="header">
              default header
            </slot>
          </div>

          <div class="modal-mask__body">
            <slot name="body">
              default body
            </slot>
          </div>

          <div class="modal-mask__footer">
            <slot name="footer">
              default footer
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
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