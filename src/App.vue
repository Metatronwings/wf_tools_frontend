<script setup>
import { NLayout, NLayoutSider, NSpace, NInputNumber, NDivider, NSwitch, NTimeline, NTimelineItem, NButton, NDatePicker } from 'naive-ui';
import { ref } from 'vue';

let free_diamond = ref()
let paid_diamond = ref()
let star_piece = ref()
let ten_pull_ticket = ref()
let single_pull_ticket = ref()
let month_card_remain_days = ref()

let small_paid_diamond_set_count = ref()
let ten_pull_ticket_count = ref()
let large_paid_diamond_set_count = ref()

let is_month_card_purchased = ref(false)

let is_daily_draw_card = ref(false)

let extra_free_diamond = ref()
let extra_paid_diamond = ref()

let total_free_diamond = ref(0)
let total_paid_diamond = ref(0)

let timestamp = ref(167241600e4)

function computeDiamonds() {
  if (free_diamond.value === undefined) {
    free_diamond.value = 0
  }
  if (single_pull_ticket.value === undefined) {
    single_pull_ticket.value = 0
  }
  if (ten_pull_ticket.value === undefined) {
    ten_pull_ticket.value = 0
  }
  if (ten_pull_ticket_count.value === undefined) {
    ten_pull_ticket_count.value = 0
  }
  if (extra_free_diamond.value === undefined) {
    extra_free_diamond.value = 0
  }
  total_free_diamond.value = free_diamond.value
    + 150 * single_pull_ticket.value
    + 1500 * (ten_pull_ticket.value)
    + computeFreeDiamonds()
    + extra_free_diamond.value
  if (paid_diamond.value === undefined) {
    paid_diamond.value = 0
  }
  if (extra_paid_diamond.value === undefined) {
    extra_paid_diamond.value = 0
  }
  total_paid_diamond.value = paid_diamond.value
    + computePaidDiamonds()
    + extra_paid_diamond.value
  console.log(total_free_diamond.value)
  console.log(total_paid_diamond.value)

  if (total_free_diamond.value >= computeConsumeDiamonds()) {
    total_free_diamond.value -= computeConsumeDiamonds()
  }
  else {
    let remain_consume_diamonds = computeConsumeDiamonds() - total_free_diamond.value
    total_free_diamond.value = 0
    total_paid_diamond.value -= remain_consume_diamonds
  }
}

function computeFreeDiamonds() {
  let today = new Date()
  let end_day = new Date(timestamp.value)
  let s1 = today.getTime(), s2 = end_day.getTime()
  let total = (s2 - s1) / 1000
  let remain_days = parseInt(total / (24 * 60 * 60))

  let ret = 0
  if (is_month_card_purchased.value) {
    ret += 50 * remain_days
  }
  // 还有每日任务的钻呢
  ret += 50 * remain_days
  // 还有工资塔的钻呢
  let remain_months = Math.floor(remain_days / 30)
  ret += 1500 * remain_months
  ret += 1500 * ten_pull_ticket_count.value * remain_months
  return ret
}

function computePaidDiamonds() {
  let today = new Date()
  let end_day = new Date(timestamp.value)
  let s1 = today.getTime(), s2 = end_day.getTime()
  let total = (s2 - s1) / 1000
  let remain_days = parseInt(total / (24 * 60 * 60))
  let remain_months = Math.floor(remain_days / 30)

  let ret = 0
  if (is_month_card_purchased.value) {
    ret += 500 * remain_months
  }
  if (small_paid_diamond_set_count.value !== undefined) {
    ret += 500 * small_paid_diamond_set_count.value * remain_months
  }
  if (large_paid_diamond_set_count.value !== undefined) {
    ret += 7500 * large_paid_diamond_set_count.value * remain_months
  }
  if (is_daily_draw_card.value) {
    ret -= 75 * remain_days
  }
  return ret
}
// 这里之后是代码生成的
let yong_qi_chi_draws = ref(0)
let yong_qi_chi_stars = ref(0)

let shui_shu_xing_chi_1_draws = ref(0)
let shui_shu_xing_chi_1_stars = ref(0)

let yong_ai_shui_gay_chi_draws = ref(0)
let yong_ai_shui_gay_chi_stars = ref(0)

let sheng_nv_deng_nai_chi_draws = ref(0)
let sheng_nv_deng_nai_chi_stars = ref(0)

let zuo_he_yi_qi_draws = ref(0)
let zuo_he_yi_qi_stars = ref(0)

let zuo_he_er_qi_draws = ref(0)
let zuo_he_er_qi_stars = ref(0)

let wan_sheng_ke_xue_jia_draws = ref(0)
let wan_sheng_ke_xue_jia_stars = ref(0)

let huo_lao_shi_draws = ref(0)
let huo_lao_shi_stars = ref(0)

let huang_nv_he_liu_ge_zi_de_feng_jue_se_draws = ref(0)
let huang_nv_he_liu_ge_zi_de_feng_jue_se_stars = ref(0)

let li_ji_draws = ref(0)
let li_ji_stars = ref(0)

let yi_zhou_nian_san_jie_draws = ref(0)
let yi_zhou_nian_san_jie_stars = ref(0)

let sheng_long_draws = ref(0)
let sheng_long_stars = ref(0)

let niu_niu_draws = ref(0)
let niu_niu_stars = ref(0)

let lei_zhi_zun_yi_ji_EMT_RE0_lian_dong_draws = ref(0)
let lei_zhi_zun_yi_ji_EMT_RE0_lian_dong_stars = ref(0)

function computeConsumeDiamonds() {
  let ret = 0
  ret += yong_qi_chi_draws.value
  ret += shui_shu_xing_chi_1_draws.value
  ret += yong_ai_shui_gay_chi_draws.value
  ret += sheng_nv_deng_nai_chi_draws.value
  ret += zuo_he_yi_qi_draws.value
  ret += zuo_he_er_qi_draws.value
  ret += wan_sheng_ke_xue_jia_draws.value
  ret += huo_lao_shi_draws.value
  ret += huang_nv_he_liu_ge_zi_de_feng_jue_se_draws.value
  ret += li_ji_draws.value
  ret += yi_zhou_nian_san_jie_draws.value
  ret += sheng_long_draws.value
  ret += niu_niu_draws.value
  ret += lei_zhi_zun_yi_ji_EMT_RE0_lian_dong_draws.value
  return 150 * ret
}
function computeConsumeStars() {
  let ret = 0
  ret += yong_qi_chi_stars.value
  ret += shui_shu_xing_chi_1_stars.value
  ret += yong_ai_shui_gay_chi_stars.value
  ret += sheng_nv_deng_nai_chi_stars.value
  ret += zuo_he_yi_qi_stars.value
  ret += zuo_he_er_qi_stars.value
  ret += wan_sheng_ke_xue_jia_stars.value
  ret += huo_lao_shi_stars.value
  ret += huang_nv_he_liu_ge_zi_de_feng_jue_se_stars.value
  ret += li_ji_stars.value
  ret += yi_zhou_nian_san_jie_stars.value
  ret += sheng_long_stars.value
  ret += niu_niu_stars.value
  ret += lei_zhi_zun_yi_ji_EMT_RE0_lian_dong_stars.value
  return ret
}

</script><template>
  <n-layout position="absolute">
    <n-layout has-sider position="absolute" style="top: 20px; bottom: 20px;">
      <n-layout-sider bordered content-style="padding: 12px;" width="40%">
        <n-space vertical>
          <n-input-number v-model:value="free_diamond" :min="0" placeholder="免费钻">
            <!-- <template #prefix>免费钻</template> -->
          </n-input-number>
          <n-input-number v-model:value="paid_diamond" :min="0" placeholder="付费钻">
            <!-- <template #prefix>付费钻</template> -->
          </n-input-number>
          <n-input-number v-model:value="star_piece" :min="0" placeholder="星碎">
            <!-- <template #prefix>星碎</template> -->
          </n-input-number>
          <n-input-number v-model:value="ten_pull_ticket" :min="0" placeholder="十连券">
            <!-- <template #prefix>十连券</template> -->
          </n-input-number>
          <n-input-number v-model:value="single_pull_ticket" :min="0" placeholder="单抽券">
            <!-- <template #prefix>单抽券</template> -->
          </n-input-number>
          <n-input-number v-model:value="month_card_remain_days" :min="0" placeholder="月卡几天到期？">
            <!-- <template #prefix>月卡几天到期？</template> -->
          </n-input-number>
          <n-divider />
          <n-switch v-model:value="is_month_card_purchased">
            <template #checked>我买月卡</template>
            <template #unchecked>我不买月卡</template>
          </n-switch>
          <n-input-number v-model:value="small_paid_diamond_set_count" :min="0" :max="8" placeholder="每月25几次？">
            <!-- <template #prefix>每月25几次？</template> -->
          </n-input-number>
          <n-input-number v-model:value="ten_pull_ticket_count" :min="0" :max="3" placeholder="每月98几次？">
            <!-- <template #prefix>每月98几次？</template> -->
          </n-input-number>
          <n-input-number v-model:value="large_paid_diamond_set_count" :min="0" :max="3" placeholder="每月518几次？">
            <!-- <template #prefix>每月518几次？</template> -->
          </n-input-number>
          <n-divider />
          <n-switch v-model:value="is_daily_draw_card">
            <template #checked>抽TM的！</template>
            <template #unchecked>我就不每日单抽</template>
          </n-switch>
          <n-input-number v-model:value="extra_free_diamond" :min="0" placeholder="额外免费钻">
            <!-- <template #prefix>额外免费钻</template> -->
          </n-input-number>
          <n-input-number v-model:value="extra_paid_diamond" :min="0" placeholder="额外付费钻">
            <!-- <template #prefix>额外付费钻</template> -->
          </n-input-number>
          <n-divider />设定一个日期然后开始计算吧！
          <n-date-picker v-model:value="timestamp" type="date" clearable />
          <n-button @click="computeDiamonds">点击计算</n-button>
          <n-space vertical>
            <n-space>等价免费钻剩余：{{ total_free_diamond }}</n-space>
            <n-space>付费钻剩余：{{ total_paid_diamond }}</n-space>
            <n-space>星碎剩余：(先占个位)</n-space>
          </n-space>
        </n-space>
      </n-layout-sider>
      <n-layout content-style="padding: 12px;" :native-scrollbar="false">
        <n-timeline>
          <n-timeline-item type="warning" title="泳奇池" time="2022-06-02">
            <n-space vertical #default>
              泳奇、泳虎，还有两个没啥用的四星。
              <n-input-number v-model:value="yong_qi_chi_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yong_qi_chi_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="info" title="水属性池1" time="2022-06-09">
            <n-space vertical #default>
              不会真有人抽属性池子吧？
              <n-input-number v-model:value="shui_shu_xing_chi_1_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="shui_shu_xing_chi_1_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="泳爱水gay池" time="2022-06-16">
            <n-space vertical #default>
              水gay，踢罐好手。
              <n-input-number v-model:value="yong_ai_shui_gay_chi_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yong_ai_shui_gay_chi_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="圣女灯奶池" time="2022-06-30">
            <n-space vertical #default>
              太强啦，可惜是两个常驻。不过仍然值得一抽。
              <n-input-number v-model:value="sheng_nv_deng_nai_chi_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="sheng_nv_deng_nai_chi_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="佐贺一期" time="2022-07-21">
            <n-space vertical #default>
              四星夕雾比较有用，余钻多可以抽一下。
              <n-input-number v-model:value="zuo_he_yi_qi_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="zuo_he_yi_qi_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="佐贺二期" time="2022-07-28">
            <n-space vertical #default>
              微氪党可以跳过。
              <n-input-number v-model:value="zuo_he_er_qi_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="zuo_he_er_qi_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="万圣科学家" time="2022-08-04">
            <n-space vertical #default>
              四星万圣科学家是大奖，值得捞一下。
              <n-input-number v-model:value="wan_sheng_ke_xue_jia_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="wan_sheng_ke_xue_jia_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="火老师" time="2022-08-18">
            <n-space vertical #default>
              一周年就要到了，微氪不要下池哦。（虽然火老师很强）
              <n-input-number v-model:value="huo_lao_shi_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="huo_lao_shi_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="皇女和六个字的风角色" time="2022-08-25">
            <n-space vertical #default>
              一周年就要到了，微氪不要下池哦。
              <n-input-number v-model:value="huang_nv_he_liu_ge_zi_de_feng_jue_se_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="huang_nv_he_liu_ge_zi_de_feng_jue_se_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="里脊" time="2022-09-25">
            <n-space vertical #default>
              理论上所有人都要下的池子。
              <n-input-number v-model:value="li_ji_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="li_ji_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="一周年三杰" time="2022-10-01">
            <n-space vertical #default>
              理论上所有人都要下井的池子。
              <n-input-number v-model:value="yi_zhou_nian_san_jie_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yi_zhou_nian_san_jie_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="圣龙" time="2022-11-01">
            <n-space vertical #default>
              一周年之后的限定连发，其一。
              <n-input-number v-model:value="sheng_long_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="sheng_long_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="牛牛" time="2022-11-14">
            <n-space vertical #default>
              一周年之后的限定连发，其二。
              <n-input-number v-model:value="niu_niu_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="niu_niu_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="蕾至尊以及EMT_RE0联动" time="2022-12-01">
            <n-space vertical #default>
              一周年之后的限定连发，其三。
              <n-input-number v-model:value="lei_zhi_zun_yi_ji_EMT_RE0_lian_dong_draws" :min="0">
                <template #prefix>多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="lei_zhi_zun_yi_ji_EMT_RE0_lian_dong_stars" :min="0">
                <template #prefix>多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
        </n-timeline>
      </n-layout>
    </n-layout>
  </n-layout>
</template>

<style>
</style>
