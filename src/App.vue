<template>
  <shell
    :title="headerTitle"
    :userfullname="user.fullname"
    :userimage="user.image"
    :navs="navs"
    >
      <div slot="right-icon">
        <router-link to="/announcement">
          <v-btn icon>
            <v-badge overlap color="orange">
              <v-icon v-if="hasNotif" slot="badge" small>more_horiz</v-icon>
              <v-icon>notifications</v-icon>
            </v-badge>
          </v-btn>
        </router-link>
      </div>
      <div slot="main-content">
        <router-view></router-view>
      </div>
  </shell>
</template>

<script>
import Shell from './components/Shell.vue'

export default {
  name: 'app',
  components: {
    'shell': Shell,
    'home': resolve=>{
      require(['./components/home/Home.vue'], homeComponent=>{
        resolve(homeComponent.default)
      })
    }
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      drawer: false,
      user: {
        image: 'http://www.gravatar.com/avatar/43ba74cbabc484e6303b935115291c22?d=mm&s=35',
        fullname: 'Nurul Irfan'
      },
      // navs: [
      //   {name: 'home', icon: 'home', title: 'FLS Guide', path: '/'},
      //   {name: 'event', icon: 'event', title: 'Acara', path: '/event'},
      //   {name: 'account', icon: 'account_circle', title: 'Akun', path: '/account'}
      // ]
    }
  },
  computed: {
    headerTitle () {
      return this.$store.state.headerTitle
    },
    navs () {
      return this.$store.state.navigations
    },
    hasNotif () {
      return this.$store.state.hasNotif
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  height: 100%;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
