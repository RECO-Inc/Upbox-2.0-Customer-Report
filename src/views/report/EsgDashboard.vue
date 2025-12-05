<script setup lang="ts">
import {ref} from "vue";
import {useI18n} from "vue-i18n";
import { X } from "lucide-vue-next";
import { Info } from "lucide-vue-next";
import {Card} from "@/components/ui/card";
import {DropdownFilter} from "@/components/ui/dropdown-filter";
import {useWasteType} from "@/composables/useWasteType";
import {Badge} from "@/components/ui/badge";

const {t} = useI18n();
const {wasteTypeDetailOptions} = useWasteType();
const wasteTypeFilter = ref<string[]>([]);
</script>

<template>
  <div class="w-full">
    <h2 class="w-full flex items-center flex-wrap gap-x-4 gap-y-2 text-size-32 font-semibold tracking-tight mb-[20px]">
      <span>업박스 고객사 에코(ESG) 리포트</span>
      <small class="text-size-14 text-base-60 font-normal">주식회사 인스파이어인티그레이티드리조트 | 2025년 10월 기준</small>
    </h2>

    <Card class="bg-base-10 rounded-sm p-[24px] mb-[20px]">
      <div class="flex items-center justify-between">
        <strong>폐기물 종류 필터를 선택해주세요</strong>
        <DropdownFilter
          v-model="wasteTypeFilter"
          :options="wasteTypeDetailOptions"
          :placeholder="t('playground.select.placeholder')"
          size="sm"
          search />
      </div>
      <div v-if="wasteTypeFilter.length" class="flex items-center gap-4 mt-4">
        <Badge v-for="item in wasteTypeFilter"
               :key="item"
               :value="item"
               class="flex items-center gap-x-2">
          <span>{{ wasteTypeDetailOptions.find(o => o.value === item)?.label ?? "-" }}</span>
          <X class="w-3 h-3 bg-base-80 text-base-10 rounded-full cursor-pointer" @click="wasteTypeFilter = wasteTypeFilter.filter(v => v !== item)" />
        </Badge>
      </div>
    </Card>

    <Card class="bg-base-10 rounded-sm p-[24px] border-none">
      <section class="mb-16">
        <h3 class="text-size-24 font-bold mb-4">2025년 10월 누적 환경 임팩트</h3>

        <!-- 지표 카드 -->
        <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-4 mb-4">
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/tanso.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">이산화탄소 감축량</span>
              </div>
              <span class="text-size-13 font-bold">4,043 MtCO2eq.</span>
            </div>
          </Card>
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/water.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">물 절약량</span>
              </div>
              <span class="text-size-13 font-bold">2416 m³H₂Oeq</span>
            </div>
          </Card>
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/energe.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">에너지 회수량</span>
              </div>
              <span class="text-size-13 font-bold">5,339 MWh</span>
            </div>
          </Card>
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/recycle.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">재활용률</span>
              </div>
              <span class="text-size-13 font-bold">TBU %</span>
            </div>
          </Card>
        </div>

        <div class="flex items-center justify-center gap-8 mb-6">
          <div class="flex items-center justify-center bg-base-20 gap-8 py-8 grow rounded-2">
            <p class="text-size-16 text-base-60 font-semibold">녹화 효과</p>
            <div class="w-[1px] h-4 bg-base-40" />
            <p class="text-size-24 text-positive-80 font-bold flex items-center gap-x-4">
              <img src="/images/tree.svg" alt="" />
              <span>112,501 그루</span>
            </p>
          </div>
          <div class="flex items-center justify-center bg-base-20 gap-8 py-8 grow rounded-2">
            <p class="text-size-16 text-base-60 font-semibold">승용차 감축 효과</p>
            <div class="w-[1px] h-4 bg-base-40" />
            <p class="text-size-24 text-info-80 font-bold flex items-center gap-x-4">
              <img src="/images/car.svg" alt="" />
              <span>873대</span>
            </p>
          </div>
        </div>

        <div>
          <p class="flex items-center gap-x-1 text-size-14 text-positive-80 font-semibold mb-2">
            <Info class="w-4 h-4" />
            <span>임팩트 산정 기준</span>
          </p>
          <ul class="text-size-14 text-base-80 list-disc pl-5">
            <li>이산화탄소 감축량: 음식물류 폐기물의 비소각 처리 및 폐플라스틱 자원화를 통해 감축된 CO₂ 환산량입니다.</li>
            <li>물 절약량: 폐기물의 소각 및 매립 공정 대신 자원순환 처리 시 절약되는 물의 양입니다.</li>
            <li>녹화/승용차 효과: 감축된 이산화탄소 양을 소나무 연간 흡수량 및 승용차 연간 배출량 기준으로 환산한 값입니다.</li>
          </ul>
        </div>
      </section>

      <section class="mb-16">
        <h3 class="text-size-24 font-bold mb-1">2025년 10월 폐기물 수거 현황</h3>
        <p class="text-base-70 mb-4">음식물류는 1L=1kg으로 환산되었으며, 그 외 모든 폐기물은 kg 단위입니다.</p>

        <div class="flex items-center justify-center bg-base-40 text-size-32 text-base-10 font-bold min-h-[540px]">
          Data area
        </div>
      </section>

      <section>
        <h3 class="text-size-24 font-bold mb-1">2025년 10월 전년 동월 대비 증감 분석 (YoY)</h3>
        <p class="text-base-70 mb-4">음식물류는 1L=1kg으로 환산되었으며, 그 외 모든 폐기물은 kg 단위입니다.</p>

        <div class="flex items-center justify-center bg-base-40 text-size-32 text-base-10 font-bold min-h-[540px]">
          Data area
        </div>
      </section>
    </Card>
  </div>
</template>

<style scoped lang="scss">

</style>