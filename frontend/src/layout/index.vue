<template>
  <el-container class="app-wrapper" :class="{ mobile: isMobile }">
    <div v-show="isMobile && !hideSidebar" class="drawer-bg" @click="hideSidebar = true"></div>
    <el-aside width="230px" class="sidebar-container" :class="{ 'hide-sidebar': hideSidebar }">
      <div class="logo-container">
        <router-link to="/">
          <img src="@/assets/img/logo.png" class="sidebar-logo">
          <h1 class="sidebar-title">blivechat</h1>
        </router-link>
      </div>
      <div class="version">
        {{ APP_VERSION }}-230709
      </div>
      <div class="version">
        <a href="https://space.bilibili.com/12236936" target="_blank">只熊KUMA</a>
      </div>
      <div class="version">
        <a href="https://www.yuque.com/doodle-irifi/ueaigm/laogg2" target="_blank" style="color: #bed742;">使用教程</a>
      </div>
      <div class="version">
        <a href="https://www.yuque.com/doodle-irifi/ueaigm/stntb3" target="_blank">下载更新/版本记录</a>
      </div>
      <div class="version">
        <a href="https://github.com/xfgryujk/blivechat/releases" target="_blank">下载原版blivechat</a>
      </div>
      <sidebar></sidebar>
    </el-aside>
    <el-main>
      <el-button v-show="isMobile" class="menu-button" icon="el-icon-s-unfold" @click="hideSidebar = false"></el-button>
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </el-main>
  </el-container>
</template>

<script>
import Sidebar from './Sidebar'

export default {
  name: 'Layout',
  components: {
    Sidebar
  },
  data() {
    return {
      APP_VERSION: process.env.APP_VERSION,

      isMobile: false,
      hideSidebar: true
    }
  },
  mounted() {
    window.addEventListener('resize', this.onResize)
    this.onResize()
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.onResize)
  },
  methods: {
    onResize() {
      this.isMobile = document.body.clientWidth <= 992
    }
  }
}
</script>

<style>
html {
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "\5FAE \8F6F \96C5 \9ED1 ", "微软雅黑", Arial, sans-serif;
}

html, body, #app, .app-wrapper, .sidebar-container {
  height: 100%;
}

body {
  margin: 0;
  background-color: #f6f8fa;
}

a, a:focus, a:hover {
  text-decoration: none;
}

.drawer-bg {
  background: #000;
  opacity: 0.3;
  width: 100%;
  top: 0;
  height: 100%;
  position: absolute;
  z-index: 999;
}

.sidebar-container {
  background-color: #304156;
  overflow: hidden;
}

.app-wrapper.mobile .sidebar-container {
  position: fixed;
  top: 0;
  left: 0;
  transition-duration: 0.3s;
  z-index: 1001;
}

.app-wrapper.mobile .sidebar-container.hide-sidebar {
  pointer-events: none;
  transition-duration: 0.3s;
  transform: translate3d(-230px, 0, 0);
}

.sidebar-container .logo-container {
  width: 100%;
  height: 50px;
  line-height: 50px;
  background: #2b2f3a;
  text-align: center;
}

.sidebar-container .logo-container .sidebar-logo {
  width: 32px;
  height: 32px;
  vertical-align: middle;
  margin-right: 12px;
}

.sidebar-container .logo-container .sidebar-title {
  display: inline-block;
  margin: 0;
  color: #fff;
  font-weight: 600;
  line-height: 50px;
  font-size: 14px;
  font-family: Avenir, Helvetica Neue, Arial, Helvetica, sans-serif;
  vertical-align: middle;
}

.sidebar-container .version {
  height: 30px;
  background: #2b2f3a;
  color: #aaa;
  font-weight: 600;
  line-height: 30px;
  font-size: 14px;
  vertical-align: middle;
  text-align: center;
}

.sidebar-container .is-horizontal {
  display: none;
}

.version a {
  color: #409eff
}

.el-aside[style="width: 230px;"] {
    width: 140px !important;
}

/* 修改布局 */
main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"]>.el-form>h3 {
    display: none !important;
}

main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"]>.el-tabs.el-tabs--top:has(#pane-general) {
    display: none !important;
}

main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"] {
    padding: 0 !important;
    width: 650px !important;
}

main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"]>.el-form>.el-card.is-never-shadow>.el-card__body {
    padding-left: 5px !important;
    padding-top: 0 !important;
    padding-bottom: 0 !important;
    padding-right: 5px !important;
}

main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"]>.el-form>.el-card.is-never-shadow>.el-card__body>.el-form-item.el-form-item--mini>.el-form-item__label[style="width: 150px;"] {
    text-align: left !important;
}

main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"]>.el-form>.el-card.is-never-shadow>.el-card__body>.el-form-item.el-form-item--mini>.el-form-item__content[style="margin-left: 150px;"] {
    padding: 0 !important;
    margin: 0 !important;
}

main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"]>.el-form>.el-card.is-never-shadow>.el-card__body>.el-form-item.el-form-item--mini>.el-form-item__content[style="margin-left: 150px;"]>.el-textarea {
    height: 850px !important;
}

main>.el-row[style="margin-left: -10px; margin-right: -10px;"]>.el-col[style="padding-left: 10px; padding-right: 10px;"]>.el-form>.el-card.is-never-shadow>.el-card__body>.el-form-item.el-form-item--mini>.el-form-item__content[style="margin-left: 150px;"]>.el-textarea>.el-textarea__inner {
    height: 100%;
    font-size: 15px !important;
    font-family: Consolas !important;
}

.el-card__body>.el-form-item+.el-form-item:has(.el-form-item__content[style="margin-left: 150px;"]) {
    display: none !important;
}

/* 修改高亮样式 */
.CodeMirror {
    font-size: 135%;
    line-height: 135%;
}

.CodeMirror-linenumber.CodeMirror-gutter-elt {
    font-size: 12px;
    padding-top: 2px;
}


.cm-s-darcula span.cm-tag {
    text-decoration: none !important;
}

.cm-s-darcula span.cm-comment {
    color: aqua;
    font-style: normal;
}

.CodeMirror-hints.darcula {
    background-color: #fff !important;
}

.CodeMirror-hints.darcula .CodeMirror-hint-active {
    color: #fff !important;
}
</style>
