<!--
 * @Author: your name
 * @Date: 2020-01-02 11:04:49
 * @LastEditTime: 2020-02-24 22:17:36
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \nuxt\components\home-head.vue
 -->
<template>
  <nav id="site-nav" :style="`background:${background};color:${color};height:${height}px`">
    <article class="content" :style="`height:${top}px;width:${width}px`">
      <section class="login-info">
        <slot name="left-con"></slot>
        <template v-if="user">
          <em>Hi, {{user.name}}</em>
          <a @click="logout">退出</a>
        </template>
        <template v-else>
          <em>喵，欢迎来天猫</em>
          <nuxt-link to="/login">请登录</nuxt-link>
          <a href>免费注册</a>
        </template>
      </section>
      <section class="quick-menu">
        <el-menu
          :default-active="activeIndex"
          class="el-menu-quick-menu"
          :style="`height: ${height}px;line-height: ${height-3}px;`"
          mode="horizontal"
          :text-color="color"
          active-text-color="#909399"
          :background-color="background"
          @select="handleSelect"
        >
          <el-submenu index="2">
            <template slot="title">
              <i>我的淘宝</i>
            </template>
            <el-menu-item
              index="2-1"
              style="font-size: 14px;height: 30px !important;line-height: 30px !important;"
            >
              <nuxt-link to="/boughtList" :style="`color:${color}`">已买到的宝贝</nuxt-link>
            </el-menu-item>
          </el-submenu>
          <el-menu-item index="shopCart">
            <i class="iconfont icongouwuchexuanzhong" :style="`color:${iconColor}`"></i>
            <i>
              购物车
              <template v-if="total">
                <em class="total">{{total}}</em>
                件
              </template>
            </i>
          </el-menu-item>
          <el-submenu index="80">
            <template slot="title">
              <i>收藏夹</i>
            </template>
          </el-submenu>
          <el-menu-item index="8">
            <i class="iconfont iconshouji" :style="`color:${iconColor}`"></i>
            <i>手机版</i>
          </el-menu-item>
          <el-menu-item index="9">
            <i>淘宝网</i>
          </el-menu-item>
          <el-submenu index="4">
            <template slot="title">
              <i>商家支持</i>
            </template>
          </el-submenu>
          <el-submenu index="10">
            <template slot="title">
              <i class="iconfont iconliebiao" :style="`color:${iconColor}`"></i>
              <i>网站导航</i>
            </template>
          </el-submenu>
        </el-menu>
      </section>
    </article>
  </nav>
</template>

<script>
export default {
  name: 'homeHead',
  props: {
    background: {
      type: String,
      default: '#f2f2f2'
    },
    top: {
      type: Number
    },
    color: {
      type: String,
      default: '#999'
    },
    height: {
      type: Number,
      default: 28
    },
    iconColor: {
      type: String,
      default: '#ff0036'
    },
    width: {
      type: Number,
      default: 1190
    }
  },
  computed: {
    user() {
      if (this.$store.getters['isAuthenticated']) {
        return this.$store.getters['currentUser']
      } else {
        false
      }
    },
    total() {
      return this.$store.state.goods.total
    }
  },
  data() {
    return {
      activeIndex: '1',
      activeIndex2: '1'
    }
  },
  methods: {
    logout() {
      this.$store.dispatch('logout')
      this.$router.push('/')
    },
    handleSelect(index) {
      if (index === 'shopCart') {
        this.$router.push('/shopCart')
      }
    }
  }
}
</script>

<style  scoped lang='scss'>
@import '@/assets/css/menu.scss';
#site-nav {
  height: 40px;
  width: 100%;
  height: 26px;
  display: flex;
  justify-content: center;
  color: #fff;
  font-family: 'Microsoft YaHei', tahoma, arial, 'Hiragino Sans GB',
    '\5b8b\4f53', sans-serif;
}
#site-nav a {
  color: inherit;
}
.content {
  display: flex;
  justify-content: space-between;
}
.login-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.login-info > * {
  margin-right: 10px;
}
.el-menu-quick-menu {
  height: 100%;
}
#site-nav {
  position: relative !important;
  border-bottom-color: transparent !important;
  z-index: 99999;
  border-bottom: 1px solid #e5e5e5;
  box-sizing: content-box;
}
* {
  box-sizing: border-box;
}
.total {
  font-weight: 700;
  font-family: Arial;
}
</style>