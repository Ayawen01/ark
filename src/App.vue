<script setup>
import 'pixi-spine';
import * as PIXI from 'pixi.js';
import { Spine } from 'pixi-spine';
import { onMounted, ref } from 'vue';

const containerRef = ref(null);
let app = null;

async function init () {
  // 初始化
  app = new PIXI.Application({
    width: window.innerWidth,
    height: window.innerHeight,
    resolution: window.devicePixelRatio || 1,
    backgroundAlpha: 0,
  });

  // 加载资源
  const resource = await PIXI.Assets.load('/irene/build_char_4009_irene.skel');

  // 构造精灵
  const irene = new Spine(resource.spineData);
  console.log(irene);
  irene.width = irene.width / 2;
  irene.height = irene.height / 2;
  irene.x = window.innerWidth / 2;
  irene.y = window.innerHeight;

  // 播放动作
  irene.state.setAnimation(0, 'Move', true);

  // 导入舞台
  app.stage.addChild(irene);
  containerRef.value.appendChild(app.view);
}

onMounted(() => {
  init();
});
</script>

<template>
  <div class="container" ref="containerRef">
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}

.container {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0);
}
</style>
