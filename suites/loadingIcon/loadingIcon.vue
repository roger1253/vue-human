<template>
  <span class="mn-loading-icon"></span>
</template>

<script>
  import Element from '../../utils/Element'
  import Vue from 'vue'
  import defaultIcon from './defaultIcon'

  let loadingIcon = defaultIcon

  export default new Element({
    name: 'mn-loading-icon',
    beforeInstalled (Vue, options) {
      if (options.icon && typeof options.icon === 'object') loadingIcon = options.icon
    },
    data () {
      return {
        icon: undefined
      }
    },
    mounted () {
      const Component = Vue.extend(loadingIcon)
      this.icon = new Component().$mount()

      this.$nextTick(() => {
        this.$el.appendChild(this.icon.$el)
      })
    },
    beforeDestroy () {
      this.$el.removeChild(this.icon.$el)
      this.icon.$destroy()
    }
  })
</script>
