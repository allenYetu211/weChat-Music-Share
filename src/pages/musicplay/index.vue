<template>
  <div>

    <div class="music__cover--img">
      <img :src="musicTargetInfo.portrait" alt="">
      <div class="music__msg">
        <p>
          {{musicTargetInfo.msg}}
        </p>
      </div>
    </div>

  </div>
</template>

<script>
  export default {
    data() {
      return {
        id: '',
        musicListInfo: '',
        musicTargetInfo: ''
      }
    },
    mounted() {
      this.id = this.$root.$mp.query.id
      this.getInitData()
    },
    methods: {
      getInitData() {
        wx.request({
          url: 'https://easy-mock.com/mock/5afc2eece5c64d22cc1ca4f3/wachat/musicinfo',
          success: (res) => {
            this.musicListInfo = res.data.data
            this.filter()
          }
        })
      },
      filter() {
        this.musicTargetInfo = this.musicListInfo[this.id]
        this.playMusic()
      },
      playMusic() {
        const backgroundAudioManager = wx.getBackgroundAudioManager()
        backgroundAudioManager.title = this.musicTargetInfo.name
        backgroundAudioManager.epname = this.musicTargetInfo.name
        backgroundAudioManager.singer = this.musicTargetInfo.title
        backgroundAudioManager.coverImgUrl = this.musicTargetInfo.portrait
        backgroundAudioManager.src = this.musicTargetInfo.mp3
      }
    }
  }
</script>

<style lang="scss" scoped>
.music__msg{
  display: flex;
  justify-content: center;
  align-content: center;
  p {
    font-size: 28rpx;
    color: #66685d;
  }
}
img {
  width: 100vw;
  height: 100vw;
}
</style>
