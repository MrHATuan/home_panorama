<template>
  <div class="top-menu">
    <nuxt-link to="/" class="logo" style="width: 46px;">
      <img src="~/assets/img/logo.svg" width="100%">
    </nuxt-link>

    <div class="project">
      <div class="project-name tc drop-shadow visible-hq" style="display: inherit;">Mr.TuanHA</div>
      <div class="project-desc tc drop-shadow visible-hq" style="display: inherit;">VN</div>
    </div>

    <div class="menu">
      <div id="btn-daynight-toggle" class="icon-btn hint-down" hint="Day/Night Toggle" @click.prevent="toggleDayNight">
        <img v-if="isDayMode" id="btn-day" class="drop-shadow" src="~/assets/img/buttons/day.svg" alt="H1-logo">
        <img v-else id="btn-night" class="drop-shadow" src="~/assets/img/buttons/night.svg">
      </div>

      <div class="icon-btn hint-down" style="" hint="Floor Plan" onclick="minimap.onToggleMiniMap(event, false)">
        <img class="drop-shadow" src="~/assets/img/buttons/map.svg">
      </div>

      <div class="icon-btn hint-down visible-hq" hint="Measure Tool" onclick="measurements.toggleMeasure()">
        <img class="drop-shadow" src="~/assets/img/buttons/measure.svg">
      </div>

      <div class="icon-btn hint-down hidden-ios" hint="Full Screen" @click.prevent="toggleFullScreen">
        <img v-if="isFullScreen" class="drop-shadow minimise" src="~/assets/img/buttons/fullscreenoff.svg">
        <img v-else class="drop-shadow maximise" src="~/assets/img/buttons/fullscreen.svg">
      </div>

      <div class="icon-btn hint-down dropdown visible-hq" hint="Menu">
        <img class="drop-shadow" src="~/assets/img/buttons/menu-dots.svg" @click.prevent="toggleDropdownMenu">

        <ul class="dropdown-menu right drop-shadow" :class="{'open animate': showDropdownMenu}">
          <li><a onclick="takeSnapshot();toggleScreen('snapshot')"><img class="icon" src="~/assets/img/buttons/camera.svg">Screenshot Tool</a></li>
          <li><a onclick="toggleScreen('share')"><img class="icon" src="~/assets/img/buttons/share.svg">Share And Embed</a></li>
          <li><a onclick="toggleScreen('help')"><img class="icon" src="~/assets/img/buttons/help.svg">Help Screen</a></li>
        </ul>
        <div v-if="showDropdownMenu" class="dropdown-menu-plate" style="display: block;" @click.prevent="toggleDropdownMenu" />
      </div>

      <div class="icon-btn hint-down hidden-hq" hint="QR Code" onclick="toggleScreen('qr-mobile')" style="display: none;">
        <img class="drop-shadow" src="~/assets/img/buttons/qr-code.svg">
      </div>

      <div class="icon-btn hint-down hidden-hq" hint="Help Screen" onclick="toggleScreen('help-mobile')" style="display: none;">
        <img class="drop-shadow" src="~/assets/img/buttons/help-white.svg">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      isDayMode: true,
      isFullScreen: false,
      showDropdownMenu: false,
    }
  },
  mounted() {
    document.addEventListener('fullscreenchange', () => {
      this.isFullScreen = document.fullScreenElement || document.webkitIsFullScreen || document.msFullscreenElement
    })
    document.addEventListener('webkitfullscreenchange', () => {
      this.isFullScreen = document.fullScreenElement || document.webkitIsFullScreen || document.msFullscreenElement
    })
    document.addEventListener('msfullscreenchange', () => {
      this.isFullScreen = document.fullScreenElement || document.webkitIsFullScreen || document.msFullscreenElement
    })
  },
  methods: {
    toggleDayNight() {
      this.isDayMode = !this.isDayMode
    },
    toggleFullScreen() {
      if (!this.isFullScreen) {
        if (document.documentElement.requestFullScreen) {
          document.documentElement.requestFullScreen()
        } else if (document.documentElement.webkitRequestFullScreen) {
          document.documentElement.webkitRequestFullScreen()
        } else if (document.documentElement.msRequestFullscreen) {
          document.documentElement.msRequestFullscreen()
        }
        return
      }

      if (document.exitFullscreen) {
        document.exitFullscreen()
      } else if (document.webkitExitFullscreen) {
        document.webkitExitFullscreen()
      } else if (document.msExitFullscreen) {
        document.msExitFullscreen();
      }
    },
    toggleDropdownMenu() {
      this.showDropdownMenu = !this.showDropdownMenu
    }
  }
}
</script>
