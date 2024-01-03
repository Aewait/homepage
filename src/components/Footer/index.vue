<template>
  <footer>
    <div class="power" v-show="!store.playerState">
      <!-- 站点信息 -->
      <span
        >Copyright&nbsp;&copy;&nbsp;{{ fullYear }}
        <a :href="footerEnv.site_url">
          {{ footerEnv.author }}
        </a>
      </span>
      <!-- 以下信息请不要修改哦 -->
      <span class="hidden"
        >&nbsp;&amp;&nbsp;Made&nbsp;by&nbsp;<a
          :href="config.github"
          target="_blank"
        >
          {{ config.author }}
        </a>
      </span>
      <!-- 部署教程 -->
      <span v-if="footerEnv.guide_page">&nbsp;&amp;
        <a :href="footerEnv.guide_page" target="_blank"
          >教程</a
        >
      </span>
      <!-- 站点备案 -->
      <span v-if="footerEnv.icp">&nbsp;&amp;
        <a href="https://beian.miit.gov.cn" target="_blank"
          >{{ footerEnv.icp }}</a
        >
      </span>
      <!-- 公安备案 -->
      <span>&nbsp;&amp;
        <img src="/images/icon/gonganbeian.png" height="15"><a
          href="https://beian.mps.gov.cn/#/query/webSearch?code=44190002007715" rel="noreferrer" target="_blank">
          粤公网安备44190002007715
        </a>
      </span>
    </div>
    <div class="lrc" v-show="store.playerState">
      <music-one theme="filled" size="18" fill="#efefef" />
      <span class="lrc-text">
        {{ store.getPlayerLrc ? store.getPlayerLrc : "这句没有歌词" }}
      </span>
      <music-one theme="filled" size="18" fill="#efefef" />
    </div>
  </footer>
</template>

<script setup>
import { MusicOne } from "@icon-park/vue-next";
import { mainStore } from "@/store";
import config from "@/../package.json";
const store = mainStore();

let fullYear = new Date().getFullYear();
let footerEnv = {
  site_url: import.meta.env.VITE_FOOTER_URL,
  author: import.meta.env.VITE_FOOTER_AUTHER,
  guide_page: import.meta.env.VITE_FOOTER_GUIDE,
  icp: import.meta.env.VITE_FOOTER_ICP,
}
</script>

<style lang="scss" scoped>
footer {
  width: 100%;
  position: absolute;
  bottom: 0;
  left: 0;
  height: 46px;
  line-height: 46px;
  text-align: center;
  backdrop-filter: blur(10px);
  background: rgb(0 0 0 / 25%);
  z-index: 0;
  animation: fade;
  -webkit-animation: fade 0.5s;
  @media (max-width: 720px) {
    font-size: 0.85rem;
  }
  @media (max-width: 480px) {
    .hidden {
      display: none;
    }
  }
  .power {
    animation: fade;
    -webkit-animation: fade 0.3s;
  }
  .lrc {
    padding: 0 20px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    animation: fade;
    -webkit-animation: fade 0.3s;
    .lrc-text {
      margin: 0 8px;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 1;
      overflow: hidden;
      word-break: break-all;
    }
    .i-icon {
      width: 18px;
      height: 18px;
      display: inherit;
    }
  }
}
</style>