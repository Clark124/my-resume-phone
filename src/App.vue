<template>
  <div id="app" ref="app">
    <v-Header :baseInfo="baseInfo" v-if="!hidden">
      <!--<vue-particles  color="#ffffff" :particleOpacity="0.7" linesColor="#ffffff" :particlesNumber="80" shapeType="circle" :particleSize="5" :linesWidth="2" :lineLinked="true" :lineOpacity="0.4" :linesDistance="150" :moveSpeed="3" :hoverEffect="true" hoverMode="grab" :clickEffect="true" clickMode="push">
      </vue-particles>-->
    </v-Header>
    <Tab v-if="!hidden"></Tab>
    <transition enter-active-class="animated fadeInLeft">  
      <router-view :skill="skill" :project="project" v-if="!hidden"></router-view>
    </transition>
    <footer v-if="!hidden">
      <p id="footer">{{desc}}</p>
    </footer>
    <RingLoader :loading="loading" :color="color" :size="size" v-if="hidden" ></RingLoader>
    <p class="loadText" v-if="hidden">loading...</p>
  </div>
</template>

<script>
import Header from './components/header/Header'
import Tab from './components/tab/Tab'
import data from './../data.json'
import RingLoader from 'vue-spinner/src/RingLoader.vue'
// import BScroll from 'better-scroll'
export default {
  name: 'app',
  data() {
    return {
      baseInfo: {},
      skill: {},
      project: {},
      hidden: true,
      color: '#03a9f4',
      size: '100px',
      loading: true,
      desc: '© 2017 Preface . All rights reserved | Design by Clark.'
    }
  },
  created() {
    this.baseInfo = data.baseInfo
    this.skill = data.skill
    this.project = data.project

  },
  mounted() {
    let _this = this
    setTimeout(function () {
      _this.hidden = false
    }, 3000)
  },
  components: {
    'v-Header': Header,
    Tab,
    RingLoader
  }
}
</script>

<style lang="scss">
#app {}

#footer {
  line-height: 40px;
  height: 40px;
  text-align: center;
  font-size: 14px;
  background: #03a9f4;
  color: #fff;
  @media only screen and (max-width: 560px) {
    font-size: 10px;
  }
}

.v-spinner {
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
  font-size: 20px;
}

.loadText {
  position: fixed;
  left: 50%;
  top: 40%;
  transform: translate(-50%,-50%)
}
</style>
