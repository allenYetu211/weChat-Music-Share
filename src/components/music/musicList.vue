<template>

  <div class="music__container">
    <div class="music__item" v-for="(group ,i) in musicData" :key="i">
      <div class="group__data">
        {{group.time}}
      </div>
      <div class="group__item" v-for="(items, c) in group.data" :key="c">
        <navigator :url="'/pages/musicplay/main?id=' + items.id">
          <div class="music__portrait">
            <img :src="items.portrait" alt=""></div>
          <div class="music__info">
            <p>
              {{items.title}} - {{items.name}}
            </p>
            <p>
              {{items.duration}}
            </p>
          </div>
        </navigator>
      </div>

    </div>
  </div>

</template>

<script>
  export default {
    data() {
      return {
        musicData: '',
        items: [
          {message: 'Foo'},
          {message: 'Bar'}
        ]
      }
    },
    mounted() {
      this.getInitData()
    },
    methods: {
      getInitData() {
        wx.request({
          url: 'https://easy-mock.com/mock/5afc2eece5c64d22cc1ca4f3/wachat/musiclist',
          success: (res) => {
            console.log(res.data.data)
            console.log(this)
            this.musicData = res.data.data
          }
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .music__item {
    margin-bottom: 40rpx;
  }
  .music__container {
    width: 100%;
  }
  .group__data {
    margin-bottom: 20rpx;
    font-size: 48rpx;
    font-weight: 600;
    color: #0e0e07;
  }
  .group__item {
    margin-bottom: 30rpx;
   border-radius: 12rpx;
   box-shadow: 2rpx 2rpx 15rpx rgba(0, 0, 0, .2);
  }
  .group__item navigator {
    display: flex;
    justify-content: flex-start;
    align-content: flex-start;
  }

  .music__info {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    margin-left: 10rpx;
    p {
      font-size: 28rpx;
      color: #66685d;
    }
  }

  .music__portrait, .music__portrait img {
    width: 150rpx;
    height: 150rpx;
  }
</style>
