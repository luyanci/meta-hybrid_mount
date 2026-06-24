<!--

    Copyright (C) 2026 YuzakiKokuban <heibanbaize@gmail.com>

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

-->
<script setup lang="ts">
import { MiuixCard, MiuixBasicComponent, MiuixText } from "miuix-vue";
import {
  RiCheckboxCircleLine,
  RiIndeterminateCircleLine,
  RiCloseCircleLine,
} from "@remixicon/vue";

interface Props {
  status: "running" | "stopped" | "error";
  label: string;
  description?: string;
  summary?: string;
}

const props = withDefaults(defineProps<Props>(), {
  status: "stopped",
  label: "",
  description: "",
  summary: "",
});

const statusConfig = {
  running: {
    bgColor: "var(--m-color-working-status-card)",
    iconColor: "var(--m-color-working-status-icon)",
  },
  stopped: {
    bgColor: "var(--m-color-secondary-container)",
    iconColor: "var(--m-color-on-secondary-container)",
  },
  error: {
    bgColor: "var(--m-color-error-container)",
    iconColor: "var(--m-color-error)",
  },
};
</script>

<template>
  <MiuixCard
    class="status-card"
    :style="{
      '--m-card-color': statusConfig[props.status].bgColor,
    }"
  >
    <MiuixBasicComponent :title="props.label" :summary="description">
      <template #bottom>
        <MiuixText v-if="summary">{{ summary }}</MiuixText>
      </template>
    </MiuixBasicComponent>
    <div class="status-card__icon">
      <RiCheckboxCircleLine
        v-if="props.status === 'running'"
        size="110px"
        :color="statusConfig[props.status].iconColor"
      />
      <RiIndeterminateCircleLine
        v-else-if="props.status === 'stopped'"
        size="110px"
        :color="statusConfig[props.status].iconColor"
      />
      <RiCloseCircleLine
        v-else-if="props.status === 'error'"
        size="110px"
        :color="statusConfig[props.status].iconColor"
      />
    </div>
  </MiuixCard>
</template>

<style scoped>
.status-card {
  padding: 0;
  overflow: visible;
  position: relative;
}
.status-card__icon {
  position: absolute;
  bottom: -32px;
  right: -22px;
}
</style>
