<template>
  <div class="poetry">
    <div class="poetry__title">給我的小可愛</div>
    <template v-for="(poetry, index) of poetryList">
      <Transition name="fade" mode="out-in">
        <PoetryBoard
          class="poetry-board"
          v-if="index <= currentIndex"
          :key="index"
          :textList="poetry"
          @typed="onTyped"
        >
        </PoetryBoard>
      </Transition>
    </template>
  </div>
</template>

<script setup lang="ts">
import { onMounted, provide, ref } from "vue"
import PoetryBoard from "./PoetryBoard.vue"

const currentIndex = ref(0)
const isTransition = ref(true)
const isPlayOver = ref(false)
provide("isPlayOver", isPlayOver)
const onTyped = () => {
  if (currentIndex.value >= poetryList.value.length - 1)
    return (isPlayOver.value = true)
  isTransition.value = false
  setTimeout(() => {
    isTransition.value = true
  }, 500)

  currentIndex.value++

  console.log("触发事件")
}

const poetryList = ref([
  ["你就像是采姑娘的小蘑菇", "虽然有时候磨人", "但是我最爱了"],
  ["想和你一起去好多地方", "去看海，去看草原", "和我一起满世界逛"],
  ["还想带你回家", "看看我出生的地方", "去吃我老家最好吃的东西"],
  ["跟你说很多小时候那里发生的事情"],
  ["虽然我也惹你生气", "也不会说情话"],
  ["但是我理不直气也壮", "狠狠缠着你", "我会慢慢改的"],
  ["以后我也会天天帮你解决问题，每天都陪在你身边,最爱你了"],
  ["今天是小可爱纪念的日子，祝我的小可爱生日快乐!", "--瘦瘦瘦瘦瘦瘦瘦瘦瘦的大狗--"]
])

onMounted(() => {})
</script>

<style lang="scss" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.poetry {
  line-height: 2;
  width: 400px;
  font-size: 16px;
  color: rgb(255, 136, 136);
  .poetry__title {
    font-size: 30px;
    font-weight: 600;
    color: rgb(255, 85, 85);
    margin-bottom: 30px;
  }
  .poetry-board {
    margin-top: 20px;
  }
}
</style>
