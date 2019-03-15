<template>
  <div>
    <div class="notification fixed"
        v-if="myShow"
        :style="setStyle">
    <div class="delete"
            v-if="!myOptions.autoClose"
            @click="close()"></div>
    <div class="content" v-html="myOptions.content">
    </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        barControl: '',
        myOptions: this.options,
        myShow: this.show
      }
    },
    props: {
      'options': {
        type: Object,
        default: {}
      },
      'show': {
        type: Boolean,
        default: false
      }
    },
    computed: {
      setStyle () {
        return {
          color: this.myOptions.textColor || '#fff',
          background: this.myOptions.backgroundColor || '#21e7b6'
        }
      },
    },
    methods: {
      close () {
        this.$emit('close') // should to emit to change parent components status
        this.myOptions = {}
      }
    },
    watch: {
      options () {
        this.myOptions = this.options
        this.barControl = ''
        this.timers.forEach((timer) => {
          window.clearTimeout(timer)
        })
        this.timers = []
        this.countdown()
      },
      show (val) {
        this.myShow = val
      }
    },
  }
</script>
