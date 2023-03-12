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

let timestamp = ref(170006400e4)

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
    ret += 100 * remain_days
  }
  // 还有每日任务的钻呢
  ret += 50 * remain_days
  // 还有工资塔的钻呢
  let remain_months = Math.floor(remain_days / 30)
  ret += 1500 * remain_months
  // 98 的钻也要算上
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

let zang_bian_ya_li_ya_draws = ref(0)
let zang_bian_ya_li_ya_stars = ref(0)

let yong_huang_nv_yong_jing_cha_yong_long_qi_jia_shui_da_nai_draws = ref(0)
let yong_huang_nv_yong_jing_cha_yong_long_qi_jia_shui_da_nai_stars = ref(0)

let long_quan_shui_tan_zhan_tie_pian_ke_chi_draws = ref(0)
let long_quan_shui_tan_zhan_tie_pian_ke_chi_stars = ref(0)

let yong_02_draws = ref(0)
let yong_02_stars = ref(0)

let shen_hai_nai_guang_wang_zi_feng_nai_huo_lang_yi_yi_bu_ming_chi_draws = ref(0)
let shen_hai_nai_guang_wang_zi_feng_nai_huo_lang_yi_yi_bu_ming_chi_stars = ref(0)

let yong_e_yong_hu_draws = ref(0)
let yong_e_yong_hu_stars = ref(0)

let liang_gong_chun_ri_ka_chi_draws = ref(0)
let liang_gong_chun_ri_ka_chi_stars = ref(0)

let yu_feng_gei_yu_hei_draws = ref(0)
let yu_feng_gei_yu_hei_stars = ref(0)

let xin_jiao_guang_da_shu_draws = ref(0)
let xin_jiao_guang_da_shu_stars = ref(0)

let gou_quan_draws = ref(0)
let gou_quan_stars = ref(0)

let wan_sheng_yi_qi_fu_ke_wan_sheng_ge_ji_wan_hua_draws = ref(0)
let wan_sheng_yi_qi_fu_ke_wan_sheng_ge_ji_wan_hua_stars = ref(0)

let wan_sheng_er_qi_wan_sheng_zou_zhe_wan_sheng_tai_mu_draws = ref(0)
let wan_sheng_er_qi_wan_sheng_zou_zhe_wan_sheng_tai_mu_stars = ref(0)

let yuki_ci_xiao_gui_draws = ref(0)
let yuki_ci_xiao_gui_stars = ref(0)

let da_lei_long_chang_zhu_draws = ref(0)
let da_lei_long_chang_zhu_stars = ref(0)

let li_chong_li_yu_li_cang_wei_fu_ke_draws = ref(0)
let li_chong_li_yu_li_cang_wei_fu_ke_stars = ref(0)

let er_zhou_nian_bai_mao_xing_chuan_draws = ref(0)
let er_zhou_nian_bai_mao_xing_chuan_stars = ref(0)

let er_zhou_nian_xing_bai_xing_bing_le_draws = ref(0)
let er_zhou_nian_xing_bai_xing_bing_le_stars = ref(0)

let sheng_dan_tu_tu_sheng_dan_bing_mo_yan_draws = ref(0)
let sheng_dan_tu_tu_sheng_dan_bing_mo_yan_stars = ref(0)

let sheng_long_sheng_a_fu_ke_draws = ref(0)
let sheng_long_sheng_a_fu_ke_stars = ref(0)

let chun_mo_nv_hu_shen_jiang_chun_sheng_nv_draws = ref(0)
let chun_mo_nv_hu_shen_jiang_chun_sheng_nv_stars = ref(0)

let chun_niu_shui_dan_huo_shu_chun_ren_yi_dui_xin_nian_jue_se_de_fu_ke_draws = ref(0)
let chun_niu_shui_dan_huo_shu_chun_ren_yi_dui_xin_nian_jue_se_de_fu_ke_stars = ref(0)

let yi_zhou_nian_quan_bu_jue_se_fu_ke_draws = ref(0)
let yi_zhou_nian_quan_bu_jue_se_fu_ke_stars = ref(0)

let lei_mu_fu_ke_draws = ref(0)
let lei_mu_fu_ke_stars = ref(0)

let PCR_xiao_xiao_tian_xin_draws = ref(0)
let PCR_xiao_xiao_tian_xin_stars = ref(0)

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
  ret += zang_bian_ya_li_ya_draws.value
  ret += yong_huang_nv_yong_jing_cha_yong_long_qi_jia_shui_da_nai_draws.value
  ret += long_quan_shui_tan_zhan_tie_pian_ke_chi_draws.value
  ret += yong_02_draws.value
  ret += shen_hai_nai_guang_wang_zi_feng_nai_huo_lang_yi_yi_bu_ming_chi_draws.value
  ret += yong_e_yong_hu_draws.value
  ret += liang_gong_chun_ri_ka_chi_draws.value
  ret += yu_feng_gei_yu_hei_draws.value
  ret += xin_jiao_guang_da_shu_draws.value
  ret += gou_quan_draws.value
  ret += wan_sheng_yi_qi_fu_ke_wan_sheng_ge_ji_wan_hua_draws.value
  ret += wan_sheng_er_qi_wan_sheng_zou_zhe_wan_sheng_tai_mu_draws.value
  ret += yuki_ci_xiao_gui_draws.value
  ret += da_lei_long_chang_zhu_draws.value
  ret += li_chong_li_yu_li_cang_wei_fu_ke_draws.value
  ret += er_zhou_nian_bai_mao_xing_chuan_draws.value
  ret += er_zhou_nian_xing_bai_xing_bing_le_draws.value
  ret += sheng_dan_tu_tu_sheng_dan_bing_mo_yan_draws.value
  ret += sheng_long_sheng_a_fu_ke_draws.value
  ret += chun_mo_nv_hu_shen_jiang_chun_sheng_nv_draws.value
  ret += chun_niu_shui_dan_huo_shu_chun_ren_yi_dui_xin_nian_jue_se_de_fu_ke_draws.value
  ret += yi_zhou_nian_quan_bu_jue_se_fu_ke_draws.value
  ret += lei_mu_fu_ke_draws.value
  ret += PCR_xiao_xiao_tian_xin_draws.value
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
  ret += zang_bian_ya_li_ya_stars.value
  ret += yong_huang_nv_yong_jing_cha_yong_long_qi_jia_shui_da_nai_stars.value
  ret += long_quan_shui_tan_zhan_tie_pian_ke_chi_stars.value
  ret += yong_02_stars.value
  ret += shen_hai_nai_guang_wang_zi_feng_nai_huo_lang_yi_yi_bu_ming_chi_stars.value
  ret += yong_e_yong_hu_stars.value
  ret += liang_gong_chun_ri_ka_chi_stars.value
  ret += yu_feng_gei_yu_hei_stars.value
  ret += xin_jiao_guang_da_shu_stars.value
  ret += gou_quan_stars.value
  ret += wan_sheng_yi_qi_fu_ke_wan_sheng_ge_ji_wan_hua_stars.value
  ret += wan_sheng_er_qi_wan_sheng_zou_zhe_wan_sheng_tai_mu_stars.value
  ret += yuki_ci_xiao_gui_stars.value
  ret += da_lei_long_chang_zhu_stars.value
  ret += li_chong_li_yu_li_cang_wei_fu_ke_stars.value
  ret += er_zhou_nian_bai_mao_xing_chuan_stars.value
  ret += er_zhou_nian_xing_bai_xing_bing_le_stars.value
  ret += sheng_dan_tu_tu_sheng_dan_bing_mo_yan_stars.value
  ret += sheng_long_sheng_a_fu_ke_stars.value
  ret += chun_mo_nv_hu_shen_jiang_chun_sheng_nv_stars.value
  ret += chun_niu_shui_dan_huo_shu_chun_ren_yi_dui_xin_nian_jue_se_de_fu_ke_stars.value
  ret += yi_zhou_nian_quan_bu_jue_se_fu_ke_stars.value
  ret += lei_mu_fu_ke_stars.value
  ret += PCR_xiao_xiao_tian_xin_stars.value
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
          <n-date-picker v-model:value="timestamp" type="date" />
          <n-button @click="computeDiamonds">
            点击计算
          </n-button>
            等价免费钻剩余：{{ total_free_diamond }}
        </n-space>
      </n-layout-sider>
      <n-layout content-style="padding: 24px;" :native-scrollbar="false">
        <n-timeline>
          <n-timeline-item type="error" title="三杰池礼鱼礼铳礼仓唯" time="2023-03-09">
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
          <n-timeline-item type="success" title="脏辫亚里亚" time="2023-04-27">
            <n-space vertical #default>
              还算OK的一个池子
              <n-input-number v-model:value="zang_bian_ya_li_ya_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="zang_bian_ya_li_ya_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="泳皇女泳警察泳龙骑加水大奶" time="2023-05-04">
            <n-space vertical #default>
              很大(泳龙骑值得一捞)
              <n-input-number v-model:value="yong_huang_nv_yong_jing_cha_yong_long_qi_jia_shui_da_nai_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yong_huang_nv_yong_jing_cha_yong_long_qi_jia_shui_da_nai_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="info" title="龙拳水碳斩铁骗氪池" time="2023-05-17">
            <n-space vertical #default>
              都是重量级但是不想抽
              <n-input-number v-model:value="long_quan_shui_tan_zhan_tie_pian_ke_chi_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="long_quan_shui_tan_zhan_tie_pian_ke_chi_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="泳02" time="2023-05-24">
            <n-space vertical #default>
              强度换立绘
              <n-input-number v-model:value="yong_02_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yong_02_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="info" title="深海奶光王子风奶火狼意义不明池" time="2023-06-06">
            <n-space vertical #default>
              意义不明
              <n-input-number v-model:value="shen_hai_nai_guang_wang_zi_feng_nai_huo_lang_yi_yi_bu_ming_chi_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="shen_hai_nai_guang_wang_zi_feng_nai_huo_lang_yi_yi_bu_ming_chi_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="泳蛾泳狐" time="2023-06-13">
            <n-space vertical #default>
              纯色风PF光PF
              <n-input-number v-model:value="yong_e_yong_hu_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yong_e_yong_hu_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="凉宫春日卡池" time="2023-06-26">
            <n-space vertical #default>
              联动限定，可捞
              <n-input-number v-model:value="liang_gong_chun_ri_ka_chi_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="liang_gong_chun_ri_ka_chi_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="浴风给浴黑" time="2023-07-09">
            <n-space vertical #default>
              一般般
              <n-input-number v-model:value="yu_feng_gei_yu_hei_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yu_feng_gei_yu_hei_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="心角光大叔" time="2023-07-22">
            <n-space vertical #default>
              常驻池，谨慎
              <n-input-number v-model:value="xin_jiao_guang_da_shu_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="xin_jiao_guang_da_shu_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="狗拳" time="2023-07-29">
            <n-space vertical #default>
              最推荐付费井拿下的卡池之一
              <n-input-number v-model:value="gou_quan_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="gou_quan_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="万圣一期复刻万圣歌姬万化" time="2023-08-11">
            <n-space vertical #default>
              万化她真的很强
              <n-input-number v-model:value="wan_sheng_yi_qi_fu_ke_wan_sheng_ge_ji_wan_hua_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="wan_sheng_yi_qi_fu_ke_wan_sheng_ge_ji_wan_hua_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="万圣二期万圣奏者万圣太母" time="2023-08-18">
            <n-space vertical #default>
              太母不太行
              <n-input-number v-model:value="wan_sheng_er_qi_wan_sheng_zou_zhe_wan_sheng_tai_mu_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="wan_sheng_er_qi_wan_sheng_zou_zhe_wan_sheng_tai_mu_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="yuki雌小鬼" time="2023-08-31">
            <n-space vertical #default>
              JKJKJKJK
              <n-input-number v-model:value="yuki_ci_xiao_gui_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yuki_ci_xiao_gui_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="info" title="大雷龙常驻" time="2023-09-07">
            <n-space vertical #default>
              大雷龙
              <n-input-number v-model:value="da_lei_long_chang_zhu_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="da_lei_long_chang_zhu_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="礼铳礼鱼礼仓唯复刻" time="2023-09-13">
            <n-space vertical #default>
              没有的可以捞下
              <n-input-number v-model:value="li_chong_li_yu_li_cang_wei_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="li_chong_li_yu_li_cang_wei_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="二周年白猫星船" time="2023-09-20">
            <n-space vertical #default>
              建议全部拿下
              <n-input-number v-model:value="er_zhou_nian_bai_mao_xing_chuan_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="er_zhou_nian_bai_mao_xing_chuan_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="二周年星白星冰乐" time="2023-10-04">
            <n-space vertical #default>
              还是不错的
              <n-input-number v-model:value="er_zhou_nian_xing_bai_xing_bing_le_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="er_zhou_nian_xing_bai_xing_bing_le_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="圣诞兔兔圣诞冰魔眼" time="2023-10-11">
            <n-space vertical #default>
              
              <n-input-number v-model:value="sheng_dan_tu_tu_sheng_dan_bing_mo_yan_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="sheng_dan_tu_tu_sheng_dan_bing_mo_yan_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="error" title="圣龙圣阿复刻" time="2023-10-18">
            <n-space vertical #default>
              
              <n-input-number v-model:value="sheng_long_sheng_a_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="sheng_long_sheng_a_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="春魔女虎神将春圣女" time="2023-10-25">
            <n-space vertical #default>
              
              <n-input-number v-model:value="chun_mo_nv_hu_shen_jiang_chun_sheng_nv_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="chun_mo_nv_hu_shen_jiang_chun_sheng_nv_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="春牛水弹火鼠春忍一堆新年角色的复刻" time="2023-11-02">
            <n-space vertical #default>
              
              <n-input-number v-model:value="chun_niu_shui_dan_huo_shu_chun_ren_yi_dui_xin_nian_jue_se_de_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="chun_niu_shui_dan_huo_shu_chun_ren_yi_dui_xin_nian_jue_se_de_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="warning" title="一周年全部角色复刻" time="2023-11-02">
            <n-space vertical #default>
              
              <n-input-number v-model:value="yi_zhou_nian_quan_bu_jue_se_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="yi_zhou_nian_quan_bu_jue_se_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="雷姆复刻" time="2023-11-09">
            <n-space vertical #default>
              
              <n-input-number v-model:value="lei_mu_fu_ke_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="lei_mu_fu_ke_stars" :min="0">
                <template #prefix>投入多少星碎？</template>
              </n-input-number>
            </n-space>
          </n-timeline-item>
          <n-timeline-item type="success" title="PCR小小甜心" time="2023-11-16">
            <n-space vertical #default>
              
              <n-input-number v-model:value="PCR_xiao_xiao_tian_xin_draws" :min="0">
                <template #prefix>投入多少抽？</template>
              </n-input-number>
              <n-input-number v-model:value="PCR_xiao_xiao_tian_xin_stars" :min="0">
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
