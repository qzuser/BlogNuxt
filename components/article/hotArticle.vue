<template>
  <div :class="mode">
    <transition-group tag="ul" name="list" mode="out-in">
      <li v-for="item in article" :key="item.id" @click="viewDetail(item.id)" >
        <!-- <div class="banner" v-if='item.cover'>
          <img :src="item.cover">
        </div> -->
        <div class="font">
          <h5>[ {{ item.articleTag }} ] {{ item.articleTitle.length > 12 ? item.articleTitle.slice(0, 12) + '....' : item.articleTitle }}</h5>
        </div>
      </li>
      <li class="backFont" v-if="!article.length" :key="Math.random()">暂无文章</li>
    </transition-group>
  </div>
</template>
<script>
export default {
  name: 'hotArticle',
  props: {
    mode: {
      type: String,
      default: 'hot-article'
    }
  },
  computed: {
    article () {
      return  this.$store.state.article.hotArticle
    }
  },
  methods: {
    viewDetail (item) {
      this.$router.push(`/article/${item}`)
    }
  },
  mounted () {
    // console.log(1)
  }
}
</script>
<style lang='scss' scoped>
.hot-article {
  width: 100%;
  ul {
    width: 100%;
    li {
      background: #fff;
      border-radius: 5px;
      cursor: pointer;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      &.backFont {
        justify-content: center;
      }
      .banner {
        min-width: 70px;
        max-width: 70px;
        height: 70px;
        margin-right: 10px;
        background-color: #cdcdcd;
        overflow: hidden;
        img {
          width: 180%;
        }
      }
      .font {
        h5 {
          font-weight: normal;
          font-size: 14px;
          margin-bottom: 5px;
        }
      }
    }
  }
}
.list {
  margin-left: 20px;
  border-left: 1px solid $border;
  padding-left: 10px;
  height: 300px;
  ul {
    width: 300px;
    li {
      background: #fff;
      border-radius: 5px;
      cursor: pointer;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      &.backFont {
        justify-content: center;
      }
      .banner {
        display: none;
      }
      .font {
        display: flex;
        h5 {
          min-width: 175px;;
          font-weight: normal;
          font-size: 14px;
          margin-bottom: 5px;
        }
      }
    }
  }
}
</style>
