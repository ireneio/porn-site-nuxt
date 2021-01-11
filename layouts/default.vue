<template>
  <div>
    <div class="header__bg">
      <div class="header container">
        <div class="header__item">HOME</div>
        <div class="header__item">PREVIEW</div>
        <div class="header__item">MODELHUB</div>
        <div class="header__item">SHOP</div>
        <div class="header__item">TOYS</div>
        <div class="header__item">SEXUAL WELLNESS</div>
        <div class="header__item">INSIGHTS</div>
        <div class="header__item">SITES</div>
        <div class="header__item">CN</div>
      </div>
    </div>
    <div class="search__bg">
      <div class="search container">
        <div class="search__logo"></div>
        <div class="search__bar">
          <input
            type="text"
            placeholder="搜索13,769,043個視頻"
            class="searchBar"
            v-model="query"
            @keydown.enter="handleSearch"
          />
          <div class="searchBar__btn" @click="handleSearch">
            <fa icon="search" class="searchBar__btnIcon"></fa>
          </div>
        </div>
        <div class="search__btnBox">
          <button class="btn btn--secondary btn--first">
            <fa icon="video" class="btn__icon--small"></fa>
            <div class="btn__text">上傳</div>
          </button>
          <button class="btn btn--primary">
            <fa icon="star" class="btn__icon--small"></fa>
            <div class="btn__text">升級</div>
          </button>
        </div>
        <div class="search__funcBox">
          <button class="link link--first">登錄</button>
          <button class="link">註冊</button>
        </div>
      </div>
    </div>
    <div class="tabs__bg">
      <div class="tabs container">
        <div class="tabs__item tabs__item--current" @click="$router.push('/')">
          首頁
        </div>
        <div class="tabs__item">
          視頻
        </div>
        <div class="tabs__item">
          分類
        </div>
        <div class="tabs__item">
          直播視頻
        </div>
        <div class="tabs__item">
          色情明星
        </div>
        <div class="tabs__item">
          MEET&FUCK
        </div>
        <div class="tabs__item">
          社區
        </div>
        <div class="tabs__item">
          照片及動圖
        </div>
      </div>
    </div>
    <div class="body__bg">
      <Nuxt v-if="$route.name !== 'index'" />
      <main class="body container" v-if="$route.name === 'index'">
        <div class="body__titleBar">
          <h3 class="body__title">全球熱門視頻</h3>
          <div class="body__titleBtn">
            <button class="link">
              <fa icon="plus" class="link__icon--small"></fa>
              <div class="link__text">更多視頻</div>
            </button>
          </div>
        </div>
        <div class="container">
          <div class="row">
            <div class="col result">
              <div class="card" v-for="item in result" :key="item.key.id" @click="handleShowVideo(item.key.id)">
                <div class="card__pic">
                  <div class="card__duration">
                    <div class="card__resolution">HD</div>
                    {{ `${Math.floor(item.duration / 60)}:${(item.duration % 60) >= 10 ? item.duration % 60 : '0' + item.duration % 60}` }}
                  </div>
                </div>
                <div class="card__title">{{ item.name }}</div>
                <div class="card__author">{{ item.sourceUrl }}</div>
                <div class="card__footer">
                  <div class="card__views">{{ (item.publishDate / 1000000000000).toFixed(1) }}M 次觀看</div>
                  <div class="card__ratings">{{ item.rating }}%</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: '',
      result: []
    }
  },
  methods: {
    async handleSearch() {
      try {
        const result = await this.$axios.get(`/search?q=${this.query === '' ? 'sex' : this.query}`)
        console.log(result)
        if (result.data.content && result.data.content.length > 0) {
          this.result = result.data.content.filter(item => item.key.kind === 'PornEntry').map((item) => {
            item.rating = Math.round(Math.random(90, 100) * 100)
            return item
          })
        }
      } catch (e) {

      }
    },
    handleShowVideo(id) {
      this.$router.push({ name: 'view', params: { id } })
    }
  },
  async created() {
    this.query = '69'
    await this.handleSearch()
  }
}
</script>

<style lang="scss" scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
}
.row {
  margin-left: -6px;
  margin-right: -6px;
}
.col {
  display: flex;
  flex-wrap: wrap;
  padding: 0 6px;
}

.header {
  display: flex;
  color: #eee;
  text-transform: uppercase;
  font-size: 14px;
  padding: 4px 0;
  &__bg {
    background-color: #000;
  }
  &__item {
    margin-right: 45px;
    cursor: pointer;
  }
}
.search {
  display: flex;
  align-items: center;
  height: 60px;
  &__bg {
    background-color:#292929;
    border-bottom: 1px solid #808080;
  }
  &__logo {
    background-image: url(/logo.png);
    width: 200px;
    height: 60px;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center center;
    cursor: pointer;
  }
  &__bar {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 400px;
    margin-left: 40px;
  }
  &__btnBox {
    display: flex;
    margin-left: 20px;
  }
  &__funcBox {
    display: flex;
    margin-left: auto;
  }
}
.searchBar {
  flex: 0 0 80%;
  height: 27px;
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
  border-right: none;
  border-color: #aaa;
  border-width: 1px;
  background-color: #808080;
  padding-left: 8px;
  color: #fff;
  &:focus {
    outline: none;
    color: #fff;
  }
  &__btn {
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 0 0 20%;
    height: 30px;
    background-color:#ffa31a;
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
    border-width: 0;
    margin-top: 1px;
    cursor: pointer;
  }
  &__btnIcon {
    height: 20px;
    width: 20px;
  }
}
.tabs {
  display: flex;
  &__bg {
    background-color: #292929;
  }
  &__item {
    font-weight: 600;
    padding: 12px 0;
    width: 200px;
    text-align: center;
    border-bottom: 4px solid #292929;
    color: #fff;
    font-size: 12px;
    cursor: pointer;
    &--current {
      border-bottom: 4px solid #ffa31a;
    }
  }
}
.body {
  min-height: calc(100vh);
  color: #fff;
  // padding-top: 40px;
  &__bg {
    background-color: #000;
  }
  &__titleBar {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  &__titleBtn {
    margin-left: auto;
  }
  &__title {
    padding: 20px 0;
    font-weight: bold;
    font-size: 20px;
  }
}

.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  padding: 6px 8px;
  border: none;
  cursor: pointer;
  &__icon {
    height: 20px;
    width: 20px;
    &--small {
      height: 16px;
      width: 16px;
    }
  }
  &__text {
    margin-left: 8px;
  }
  &--first {
    margin-right: 8px;
  }
  &--primary {
    background-color: #ffa31a;
    color: #000;
  }
  &--secondary {
    background-color: #1b1b1b;
    color: #fff;
  }
}
.link {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #808080;
  padding: 6px;
  border: none;
  background-color: transparent;
  font-size: 14px;
  cursor: pointer;
  &__icon {
    height: 20px;
    width: 20px;
    &--small {
      height: 16px;
      width: 16px;
    }
  }
  &__text {
    margin-left: 4px;
  }
  &--lg {
    font-size: 16PX;
  }
  &--first {
    margin-right: 16px;
  }
}
.card {
  cursor: pointer;
  width: 268px;
  min-height: 250px;
  margin-bottom: 8px;
  padding-right: 8px;
  // &:not(:first-child) {
  //   margin-left: 12px;
  // }
  &__pic {
    position: relative;
    width: 260px;
    height: 150px;
    background-image: url(/pornPlaceholder.png);
    background-size: cover;
    background-position: center center;
    background-repeat: no-repeat;
  }
  &__title,
  &__author,
  &__footer {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    width: 100%;
  }
  &__title {
    font-size: 18px;
    color: #fff;
  }
  &__author,
  &__footer {
    font-size: 14px;
    color: #808080;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    width: 100%;
  }
  &__footer {
    display: flex;
    align-items: center;
  }
  &__ratings {
    margin-left: 6px;
  }
  &__duration {
    display: flex;
    position: absolute;
    bottom: 4px;
    right: 4px;
    color: #fff;
    font-size: 14px;
  }
  &__resolution {
    margin-right: 4px;
    font-weight: bold;
  }
}

::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: #ccc;
  opacity: 1; /* Firefox */
}

:-ms-input-placeholder { /* Internet Explorer 10-11 */
  color: #ccc;
}

::-ms-input-placeholder { /* Microsoft Edge */
  color: #ccc;
}
</style>
