<template>
  <v-app>
    <v-system-bar
      height="30"
    >
      <transition name="fade">
        <div v-if="!connected" style="position: absolute; left: 50%;">
          <div style="color: grey; position: relative; left: -50%; font-size: 10px">
            Hors connexion
          </div>
        </div>
      </transition>
      <v-icon>mdi-calendar</v-icon>
      Planning IUT
      <v-spacer />
      <v-icon>mdi-school</v-icon>
      <span>{{ time }}</span>
    </v-system-bar>
    <v-main>
      <v-container fluid>
        <nuxt keep-alive />
      </v-container>
    </v-main>
    <v-footer
      absolute
      app
    >
      <span>Noéwen (<a
        href="https://twitter.com/kop_of_tea"
        :style="$vuetify.theme.dark ? 'color: white' : 'color: black'"
      >@kernoeb</a>) | {{ new Date().getFullYear() }}</span>
      <v-spacer />
      <v-tooltip top>
        <template v-slot:activator="{ on, attrs }">
          <a
            v-bind="attrs"
            href="https://brave.com/ker880"
            rel="noopener noreferrer"
            style="display: block; margin-top: 8px;"
            target="_blank"
            v-on="on"
          >
            <brave-icon class="mr-4" size="18" :style="$vuetify.theme.dark ? 'fill: whitesmoke' : 'fill: black'" />
          </a>
        </template>
        <span>Referral Brave</span>
      </v-tooltip>
      <v-tooltip top>
        <template v-slot:activator="{ on, attrs }">
          <a
            v-bind="attrs"
            href="https://paypal.me/kernoeb"
            rel="noopener noreferrer"
            style="display: block; margin-top: 8px;"
            target="_blank"
            v-on="on"
          >
            <pay-pal-icon class="mr-4" size="18" :style="$vuetify.theme.dark ? 'fill: whitesmoke' : 'fill: black'" />
          </a>
        </template>
        <span>Faire un don</span>
      </v-tooltip>
      <v-tooltip top>
        <template v-slot:activator="{ on, attrs }">
          <a
            v-bind="attrs"
            href="https://twitter.com/kop_of_tea"
            rel="noopener noreferrer"
            style="display: block; margin-top: 8px;"
            target="_blank"
            v-on="on"
          >
            <twitter-icon class="mr-4" size="18" :style="$vuetify.theme.dark ? 'fill: whitesmoke' : 'fill: black'" />
          </a>
        </template>
        <span>Twitter</span>
      </v-tooltip>
      <v-tooltip top>
        <template v-slot:activator="{ on, attrs }">
          <a
            v-bind="attrs"
            href="https://github.com/kernoeb/planningiut"
            rel="noopener noreferrer"
            style="display: block; margin-top: 8px;"
            target="_blank"
            v-on="on"
          >
            <git-hub-icon size="18" :style="$vuetify.theme.dark ? 'fill: whitesmoke' : 'fill: black'" />
          </a>
        </template>
        <span>Page du projet</span>
      </v-tooltip>
    </v-footer>
  </v-app>
</template>

<script>
import { TwitterIcon, PayPalIcon, BraveIcon, GitHubIcon } from 'vue-simple-icons'

export default {
  components: {
    TwitterIcon,
    PayPalIcon,
    BraveIcon,
    GitHubIcon
  },
  data () {
    return {
      connected: true,
      mounted: false,
      time: '',
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        }
      ],
      title: 'Planning IUT'
    }
  },
  mounted () {
    this.mounted = true

    if (!navigator.onLine) {
      this.connected = false
    }

    window.addEventListener('offline', () => {
      this.connected = false
    })

    window.addEventListener('online', () => {
      this.connected = true
    })
  },
  created () {
    this.time = this.getTime()
    setInterval(() => {
      this.time = this.getTime()
    }, 1000)
  },
  methods: {
    getTime () {
      const tmp = new Date()
      return (tmp.getHours() < 10 ? '0' : '') + tmp.getHours() + ':' + (tmp.getMinutes() < 10 ? '0' : '') + tmp.getMinutes() + ':' + (tmp.getSeconds() < 10 ? '0' : '') + tmp.getSeconds()
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
