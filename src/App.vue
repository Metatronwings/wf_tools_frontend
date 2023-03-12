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
    + 1500 * (ten_pull_ticket.value + ten_pull_ticket_count.value)
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
let san_jie_chi_li_yu_li_chong_li_cang_wei_draws = ref(0)
let san_jie_chi_li_yu_li_chong_li_cang_wei_stars = ref(0)

let si_jie_chi_li_ji_li_yu_li_chong_li_cang_wei_draws = ref(0)
let si_jie_chi_li_ji_li_yu_li_chong_li_cang_wei_stars = ref(0)

let lei_mo_nv_yong_qi_yong_hu_fu_ke_draws = ref(0)
let lei_mo_nv_yong_qi_yong_hu_fu_ke_stars = ref(0)

let shui_wang_zi_yong_ai_fu_ke_draws = ref(0)
let shui_wang_zi_yong_ai_fu_ke_stars = ref(0)

let zuo_he_fu_ke_si_he_yi_draws = ref(0)
let zuo_he_fu_ke_si_he_yi_stars = ref(0)

let guang_pao_sheng_nv_chang_zhu_pian_ke_draws = ref(0)
let guang_pao_sheng_nv_chang_zhu_pian_ke_stars = ref(0)

let chun_niu_fu_ke_draws = ref(0)
let chun_niu_fu_ke_stars = ref(0)

let huo_shu_e_zi_lao_nan_ren_deng_nai_pian_ke_draws = ref(0)
let huo_shu_e_zi_lao_nan_ren_deng_nai_pian_ke_stars = ref(0)

function computeConsumeDiamonds() {
  let ret = 0
  ret += san_jie_chi_li_yu_li_chong_li_cang_wei_draws.value
  ret += si_jie_chi_li_ji_li_yu_li_chong_li_cang_wei_draws.value
  ret += lei_mo_nv_yong_qi_yong_hu_fu_ke_draws.value
  ret += shui_wang_zi_yong_ai_fu_ke_draws.value
  ret += zuo_he_fu_ke_si_he_yi_draws.value
  ret += guang_pao_sheng_nv_chang_zhu_pian_ke_draws.value
  ret += chun_niu_fu_ke_draws.value
  ret += huo_shu_e_zi_lao_nan_ren_deng_nai_pian_ke_draws.value
  return 150 * ret
}
function computeConsumeStars() {
  let ret = 0
  ret += san_jie_chi_li_yu_li_chong_li_cang_wei_stars.value
  ret += si_jie_chi_li_ji_li_yu_li_chong_li_cang_wei_stars.value
  ret += lei_mo_nv_yong_qi_yong_hu_fu_ke_stars.value
  ret += shui_wang_zi_yong_ai_fu_ke_stars.value
  ret += zuo_he_fu_ke_si_he_yi_stars.value
  ret += guang_pao_sheng_nv_chang_zhu_pian_ke_stars.value
  ret += chun_niu_fu_ke_stars.value
  ret += huo_shu_e_zi_lao_nan_ren_deng_nai_pian_ke_stars.value
  return ret
}

</script><template>
  <n-layout position="absolute">
    <n-layout has-sider position="absolute" style="top: 20px; bottom: 20px;">
      <n-layout-sider bordered content-style="padding: 24px;" width="30%">
        <n-space vertical>
          <n-input-number v-model:value="free_diamond" :min="0">
            <template #prefix>免费钻</template>
          </n-input-number>
          <n-input-number v-model:value="paid_diamond" :min="0">
            <template #prefix>付费钻</template>
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
          <n-input-number v-model:value="month_card_remain_days" :min="0">
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
          <n-divider />
          <n-button @click="computeDiamonds">
            点击计算
          </n-button>
            等价免费钻剩余：{{ total_free_diamond }}
        </n-space>
      </n-layout-sider>
      <n-layout content-style="padding: 24px;" :native-scrollbar="false">
        <n-timeline>
          <n-timeline-item type="error" title="三杰池礼鱼礼铳礼仓唯" time="2023-03-20">
            <n-space vertical #default>
              1.5周年三杰
              <n-input-number v-model:value="san_jie_chi_li_yu_li_chong_li_cang_wei_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="san_jie_chi_li_yu_li_chong_li_cang_wei_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="四杰池礼机礼鱼礼铳礼仓唯" time="2023-03-20">
            <n-space vertical #default>
              1.5周年三杰加礼机
              <n-input-number v-model:value="si_jie_chi_li_ji_li_yu_li_chong_li_cang_wei_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="si_jie_chi_li_ji_li_yu_li_chong_li_cang_wei_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="雷魔女泳奇泳虎复刻" time="2023-03-23">
            <n-space vertical #default>
              拿下雷魔女就在今天
              <n-input-number v-model:value="lei_mo_nv_yong_qi_yong_hu_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="lei_mo_nv_yong_qi_yong_hu_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="info" title="水王子泳爱复刻" time="2023-03-30">
            <n-space vertical #default>
              没啥用的池子
              <n-input-number v-model:value="shui_wang_zi_yong_ai_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="shui_wang_zi_yong_ai_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="佐贺复刻四合一" time="2023-04-06">
            <n-space vertical #default>
              佐贺厨可抽
              <n-input-number v-model:value="zuo_he_fu_ke_si_he_yi_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="zuo_he_fu_ke_si_he_yi_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="info" title="光炮圣女常驻骗氪" time="2023-04-13">
            <n-space vertical #default>
              不抽
              <n-input-number v-model:value="guang_pao_sheng_nv_chang_zhu_pian_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="guang_pao_sheng_nv_chang_zhu_pian_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="春牛复刻" time="2023-04-20">
            <n-space vertical #default>
              没有牛牛的赶紧拿下
              <n-input-number v-model:value="chun_niu_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="chun_niu_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="info" title="火鼠蛾子老男人灯奶骗氪" time="2023-04-27">
            <n-space vertical #default>
              真的不想抽啊
              <n-input-number v-model:value="huo_shu_e_zi_lao_nan_ren_deng_nai_pian_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="huo_shu_e_zi_lao_nan_ren_deng_nai_pian_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
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
