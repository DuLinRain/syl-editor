<template>
  <div class="drop-list-item font-names-list" v-show="stated.showDropList" :style="style">
      <ul class="font-list">
        <li class="font-name" v-for="font in fonts" :key="font" :class="[ (stated.value == font) ? 'active' : '']">
            <a href="javascript:;"
              @click="handleSelect($event, font)"
              >
              <span>{{ font }}</span>
            </a>
          </li>
      </ul>
  </div>
</template>

<script>
import Config from '../../config/index'

export default {
    data() {
      let fonts = Config.getConfig('fontName')
      return {
        fonts
      }
    },
    watch: {
      // 'show': function(val) {
      //   console.log('name'+ val)
      //   if(!val) {
      //     this.$store.dispatch('getNodePosition', {})
      //   }
      // }
    },
    computed: {
      stated: function() {
        return this.$store.state.menuBar.fontName
      },
      // show: function() {
      //   return this.stated.showDropList
      // },
      style: function() {
        let position = this.$store.state.position
        return {
          top: position.bottom + 'px',
          left: position.left + 'px'
        }
      }
    },
    methods: {
      handleSelect($event, font) {
        this.$store.dispatch('updateSelectValue', {
          name: 'fontName',
          value: font
        })
        this.$store.dispatch('execCommand', {
          name: 'fontName',
          value: font
        })
        this.$store.dispatch('showDropList');
      }
    },
    mounted() {
      this.$store.dispatch('updateSelectValue', {
        name: 'fontName',
        value: this.value || this.fonts[0]
      })
    }
}
</script>

<style lang="scss" scoped>
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  .font-name {
    padding: 5px;
    &.active, &:hover {
      background: #eee;
    }
  }
</style>
