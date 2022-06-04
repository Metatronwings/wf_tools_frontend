<script setup>
import { NLayout, NLayoutSider, NH2, NSpace, NInputNumber, NDivider, NSwitch, NTimeline, NTimelineItem, NButton } from 'naive-ui'
import { ref } from 'vue';

let paid_diamond = ref()
let free_diamond = ref()
let star_piece = ref()

let test = ref("111")

let is_month_card_purchased = ref(false)

let small_paid_diamond_set_count = ref()
let ten_pull_ticket_count = ref()
let large_paid_diamond_set_count = ref()

let is_daily_draw_card = ref(false)

let extra_free_diamond = ref()
let extra_paid_diamond = ref()

</script>

<template>
  <n-layout position="absolute">
    <n-layout has-sider position="absolute" style="top: 20px; bottom: 20px;">
      <n-layout-sider bordered content-style="padding: 24px;" width="30%">
        <n-space vertical>
          <n-input-number v-model:value="paid_diamond" :min="0">
            <template #prefix>付费钻</template>
          </n-input-number>
          <n-input-number v-model:value="free_diamond" :min="0">
            <template #prefix>免费钻</template>
          </n-input-number>
          <n-input-number v-model:value="star_piece" :min="0">
            <template #prefix>星碎</template>
          </n-input-number>
          <n-input-number v-model:value="ten_pull_ticket" :min="0">
            <template #prefix>十连券</template>
          </n-input-number>
          <n-input-number v-model:value="single_pull_ticket" :min="0">
            <template #prefix>单抽券</template>
          </n-input-number>
          <n-input-number v-model:value="single_pull_ticket" :min="0">
            <template #prefix>月卡还有几天到期？</template>
          </n-input-number>
          <n-divider />
          <n-switch v-model:value="is_month_card_purchased">
            <template #checked>我买月卡</template>
            <template #unchecked>我不买月卡</template>
          </n-switch>
          <n-input-number v-model:value="small_paid_diamond_set_count" :min="0">
            <template #prefix>每个月 25 买几次？</template>
          </n-input-number>
          <n-input-number v-model:value="ten_pull_ticket_count" :min="0">
            <template #prefix>每个月 98 买几次？</template>
          </n-input-number>
          <n-input-number v-model:value="large_paid_diamond_set_count" :min="0">
            <template #prefix>每个月 518 买几次？</template>
          </n-input-number>
          <n-divider />
          <n-switch v-model:value="is_daily_draw_card">
            <template #checked>抽TM的！</template>
            <template #unchecked>我就不每日单抽</template>
          </n-switch>
          <n-input-number v-model:value="extra_free_diamond" :min="0">
            <template #prefix>额外免费钻</template>
          </n-input-number>
          <n-input-number v-model:value="extra_paid_diamond" :min="0">
            <template #prefix>额外付费钻</template>
          </n-input-number>
        </n-space>
      </n-layout-sider>
      <n-layout content-style="padding: 24px;" :native-scrollbar="false">
        <n-timeline>
          <n-timeline-item type="warning" title="泳奇池" time="2022-06-02">
            <n-space vertical #default>
              泳奇、泳虎、还有两个没啥用的四星。
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
              <n-button type="primary">确认！</n-button>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="default" title="水属性池" time="2022-06-09">
            <n-space vertical #default>
              不会真有人抽属性池子吧？
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
              <n-button type="primary">确认！</n-button>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="泳爱水gay池" time="2022-06-16">
            <n-space vertical #default>
              水gay，踢罐好手。这个池子大奖反而是四星呢。
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
              <n-button type="primary">确认！</n-button>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="圣女灯奶池" time="2022-06-16">
            <n-space vertical #default>
              太强啦，可惜是常驻。
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="free_diamond" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
              <n-button type="primary">确认！</n-button>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="警告" content="哪里警告" time="2018-04-03 20:46" />
          <n-timeline-item
            type="info"
            title="信息"
            content="是的"
            time="2018-04-03 20:46"
            line-type="dashed"
          />
          <n-timeline-item content="啊啊啊" />
        </n-timeline>
      </n-layout>
    </n-layout>
  </n-layout>
</template>

<style>
</style>