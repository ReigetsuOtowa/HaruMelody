<template>
  <div class="setting-type">
    <div class="set-list">
      <n-h3 prefix="bar"> 关于软件 </n-h3>
      <n-card class="set-item">
        <n-flex align="center" class="about">
          <SvgIcon name="SPlayer" size="26" />
          <n-text class="logo-name">HaruMelody</n-text>
          <n-tag :bordered="false" size="small" type="primary">
            {{ packageJson.version }}
          </n-tag>
        </n-flex>
      </n-card>
    </div>
    
    <div class="set-list">
      <n-h3 prefix="bar"> 小组成员 </n-h3>
      <n-flex class="link">
        <n-card
          v-for="(item, index) in groupMember"
          :key="index"
          class="link-item"
          hoverable
        >
          <n-text class="name"> {{ item.name }} </n-text>
        </n-card>
      </n-flex>
    </div>
    <div class="set-list">
      <n-h3 prefix="bar"> 原开源仓库 </n-h3>
      <n-flex class="link">
        <n-card
          v-for="(item, index) in communityData"
          :key="index"
          class="link-item"
          hoverable
          @click="openLink(item.url)"
        >
          <SvgIcon :name="item.icon" :size="26" />
          <n-text class="name"> {{ item.name }} </n-text>
        </n-card>
      </n-flex>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { UpdateLogType } from "@/types/main";
import { getUpdateLog, openLink } from "@/utils/helper";
import packageJson from "@/../package.json";

// 社区数据
const communityData = [
  {
    name: "GitHub",
    url: packageJson.github,
    icon: "Github",
  },
];

// 小组成员数据
const groupMember = [
  {
    name: "Member1",
  },
  {
    name: "Member2",
  },
  {
    name: "Member3",
  },
  {
    name: "Member4",
  },
  {
    name: "Member5",
  },
];

// 更新日志数据
const updateData = ref<UpdateLogType[] | null>(null);

// 获取更新日志
const getUpdateData = async () => (updateData.value = await getUpdateLog());

onMounted(getUpdateData);
</script>

<style lang="scss" scoped>
.about {
  .logo-name {
    font-size: 16px;
  }
  .n-tag {
    border-radius: 6px;
  }
}
.update-data {
  :deep(.n-card__content) {
    flex-direction: column !important;
    align-items: normal !important;
  }
  .version {
    padding-left: 4px;
    .n-tag {
      pointer-events: none;
      border-radius: 6px;
    }
    .time {
      margin-left: auto;
      font-size: 13px;
    }
  }
}
.link {
  .link-item {
    max-width: 200px;
    border-radius: 8px;
    cursor: pointer;
    :deep(.n-card__content) {
      display: flex;
      align-items: center;
      padding: 12px;
    }
    .n-icon {
      margin-right: 6px;
    }
  }
}
</style>
