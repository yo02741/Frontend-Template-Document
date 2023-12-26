# 當前時間 Current Local Timer

<div data-full-width="true">

<figure><img src="../../../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

</div>

```javascript
<script setup>
const nowTimer = ref(null);
const nowDate = ref("");
const nowTime = ref("");

const updateClock = () => {
  const now = new Date();

  const formatter = (payload) => payload.toString().padStart(2, "0");

  const year = now.getFullYear();
  const month = formatter(now.getMonth() + 1);
  const date = formatter(now.getDate());
  const weekday = new Intl.DateTimeFormat("zh-TW", { weekday: "long" }).format(
    now
  );

  const hours = formatter(now.getHours());
  const minutes = formatter(now.getMinutes());

  nowDate.value = `${year}/${month}/${date} ${weekday}`;
  nowTime.value = `${hours}:${minutes}`;
};

onMounted(() => {
  updateClock();
  nowTimer.value = setInterval(updateClock, 1000);
});

onBeforeUnmount(() => {
  clearInterval(nowTimer.value);
});
</script>

<template>
  <span class="now-datetime">
    <span class="now-date">{{ nowDate }}</span>
    <span class="now-time">{{ nowTime }}</span>
  </span>
</template>

<style lang="scss" scoped>
.now-datetime {
  display: flex;
  align-items: center;
  gap: 5px;
  height: 100%;
  padding: 0 15px;
  font-size: var(--el-font-size-extra-large);
}

.now-date {
  opacity: 0.75;
}
</style>

```
