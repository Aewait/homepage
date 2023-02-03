<template>
  <div class="time-capsule">
    <div class="title">
      <hourglass-full
        theme="two-tone"
        size="24"
        :fill="['#efefef', '#00000020']"
      />
      <span>时光胶囊</span>
    </div>
    <span class="text"
      >今日已经度过了&nbsp;{{ timeData.day.start }}&nbsp;小时</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.day.pass"
    />
    <span class="text"
      >本周已经度过了&nbsp;{{ timeData.week.start }}&nbsp;天</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.week.pass"
    />
    <span class="text"
      >本月已经度过了&nbsp;{{ timeData.month.start }}&nbsp;天</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.month.pass"
    />
    <span class="text"
      >今年已经度过了&nbsp;{{ timeData.year.start }}&nbsp;个月</span
    >
    <el-progress
      :text-inside="true"
      :stroke-width="20"
      :percentage="timeData.year.pass"
    />
    <span v-if="startDate">
      <span class="text">
        <p id="htmer_time">{{ startDateText }}</p>
      </span>
    </span>
  </div>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref } from "vue";
import { HourglassFull } from "@icon-park/vue-next";
import { getTimeCapsule } from "@/utils/getTime.js";

// 进度条数据
let timeData = ref(getTimeCapsule());
let timeInterval = null;

onMounted(() => {
  timeInterval = setInterval(() => {
    timeData.value = getTimeCapsule();
  }, 1000);
});

onBeforeUnmount(() => {
  clearInterval(timeInterval);
});

let startDate = ref(import.meta.env.VITE_SITE_START);
let startDateText = ref(null);

// 建站日期统计函数
const siteDateStatistics = (startDate) => {
    const currentDate = new Date();
    const differenceInTime = currentDate.getTime() - startDate.getTime();
    const differenceInDays = differenceInTime / (1000 * 3600 * 24);
    const differenceInMonths = differenceInDays / 30;
    const differenceInYears = differenceInMonths / 12;
    if (differenceInYears >= 1) {
        return `本站已经苟活了 ${Math.floor(differenceInYears)} 年 ${Math.floor(differenceInMonths % 12)} 月 ${Math.round(differenceInDays % 30)} 天`;
    } else if (differenceInMonths >= 1) {
        return `本站已经苟活了 ${Math.floor(differenceInMonths)} 月 ${Math.round(differenceInDays % 30)} 天`;
    } else {
        return `本站已经苟活了 ${Math.round(differenceInDays)} 天`;
    }
}

onMounted(() => {
    startDateText.value = siteDateStatistics(new Date(startDate.value));
});
</script>

<style lang="scss" scoped>
.time-capsule {
  width: 100%;
  .title {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin: 0.2rem 0 1.5rem;
    font-size: 1.1rem;
    .i-icon {
      display: flex;
      justify-content: center;
      align-items: center;
      margin-right: 6px;
    }
  }
  .text {
    display: block;
    margin: 1rem 0rem 0.5rem 0rem;
    font-size: 0.95rem;
  }
}
</style>