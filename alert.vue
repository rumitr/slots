<template>
  <div id="app">
    <div class="mask"></div>
    <main>
      <h1>Yummy Notie!</h1>
      <div class="btns">
        <a class="btn"
           v-for="(item, index) in btns"
           @click="notice(item.options)">{{ item.content }}</a>
      </div>
    </main>
    <notification
      :options.sync="options"
      :show.sync="showNotification" @close="closeNotification"></notification>
  </div>
</template>

<script>
  import Notification from './components/Notification'
  export default {
    name: 'app',
    components: {Notification},
    data () {
      return {
        showNotification: false,
        options: {},
        btns: [
          {
            content: 'success',
            options: {
              autoClose: false,
              content: 'Uhh...it tastes yummy!'
            }
          },
          {
            content: 'warning',
            options: {
              autoClose: false,
              backgroundColor: '#fbff7c',
              textColor: '#92253f',
              content: 'You can also customerize the background color and text color.'
            }
          },
          {
            content: 'error',
            options: {
              autoClose: true,
              backgroundColor: '#fc5050',
              content: 'Yummy notie can be closed automatically.'
            }
          },
          {
            content: 'info',
            options: {
              autoClose: true,
              showTime: 5000,
              backgroundColor: '#769FCD',
              content: 'There is an optional countdown bar for the auto close mode.',
              countdownBar: true,
              barColor: '#415F77'
            }
          },
          {
            content: 'flexible',
            options: {
              backgroundColor: 'rgba(6,45,146,.6)',
              content: `<P><span style="font-family: anana;font-size: 1.5rem">Yummy notie</span> is extremely flexible! You can use HTML to make any kind of notification.<br><i><a href="https://github.com/Yuyz0112/vue-notie">More information.</a></i></P>`,
              textColor: '#03D6D2'
            }
          }
        ]
      }
    },
    methods: {
      notice (options) {
        this.showNotification = true
        this.options = options
      },
      closeNotification () {
          this.showNotification = false
      }
    }
  }
</script>