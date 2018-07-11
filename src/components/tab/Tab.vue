<template>
    <div class="tab-item" @click.stop="check">
        <Icon :type="icon" class="tab-item-icon" />
        <span><slot></slot></span>
        <Icon v-if="closable" type="ios-close-empty" class="tab-item-close-icon" @click.native.stop="close"/>
    </div>
</template>

<script>
export default {
  name: 'Tab',
  props: {
    closable: {
      type: Boolean,
      default: false
    },
    icon: {
      type: String,
      default: 'navicon-round'
    },
    name: {
        type: [String, Number]
    },
  },
  methods: {
    close(event) {
      if (this.name === undefined) {
        this.$emit('on-close', event)
      } else {
        this.$emit('on-close', event, this.name)
      }
    },
    check() {
      if (!this.checkable) return;
      const checked = !this.isChecked
      this.isChecked = checked
      if (this.name === undefined) {
        this.$emit('on-change', checked)
      } else {
        this.$emit('on-change', checked, this.name)
      }
    }
  }
}
</script>

<style lang="less">
  @import './tab.less';
</style>
