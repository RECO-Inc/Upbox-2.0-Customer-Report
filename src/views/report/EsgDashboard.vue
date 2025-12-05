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

// TODO: 실제 데이터로 대체 필요
const companyName = '주식회사 인스파이어인티그레이티드리조트';
const reportDate = '2025년 10월';
</script>

<template>
  <div class="w-full">
    <h2 class="w-full flex items-center flex-wrap gap-x-4 gap-y-2 text-size-32 font-semibold tracking-tight mb-[20px]">
      <span>{{ t('esgDashboard.title') }}</span>
      <small class="text-size-14 text-base-60 font-normal">{{ t('esgDashboard.companyInfo', { company: companyName, date: reportDate }) }}</small>
    </h2>

    <Card class="bg-base-10 rounded-sm p-[24px] mb-[20px]">
      <div class="flex items-center justify-between">
        <strong>{{ t('esgDashboard.filter.title') }}</strong>
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
        <h3 class="text-size-24 font-bold mb-4">{{ t('esgDashboard.impact.title', { date: reportDate }) }}</h3>

        <!-- 지표 카드 -->
        <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-4 mb-4">
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/tanso.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">{{ t('esgDashboard.impact.co2Reduction') }}</span>
              </div>
              <span class="text-size-13 font-bold">4,043 MtCO2eq.</span>
            </div>
          </Card>
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/water.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">{{ t('esgDashboard.impact.waterSaving') }}</span>
              </div>
              <span class="text-size-13 font-bold">2416 m³H₂Oeq</span>
            </div>
          </Card>
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/energe.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">{{ t('esgDashboard.impact.energyRecovery') }}</span>
              </div>
              <span class="text-size-13 font-bold">5,339 MWh</span>
            </div>
          </Card>
          <Card class="bg-white border border-base-20 rounded-sm shadow-none p-5">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-x-2">
                <img src="/images/recycle.svg" alt="" />
                <span class="text-size-13 text-base-60 font-bold">{{ t('esgDashboard.impact.recyclingRate') }}</span>
              </div>
              <span class="text-size-13 font-bold">TBU %</span>
            </div>
          </Card>
        </div>

        <div class="flex items-center justify-center gap-8 mb-6">
          <div class="flex items-center justify-center bg-base-20 gap-8 py-8 grow rounded-2">
            <p class="text-size-16 text-base-60 font-semibold">{{ t('esgDashboard.impact.greeningEffect') }}</p>
            <div class="w-[1px] h-4 bg-base-40" />
            <p class="text-size-24 text-positive-80 font-bold flex items-center gap-x-4">
              <img src="/images/tree.svg" alt="" />
              <span>{{ t('esgDashboard.impact.trees', { count: '112,501' }) }}</span>
            </p>
          </div>
          <div class="flex items-center justify-center bg-base-20 gap-8 py-8 grow rounded-2">
            <p class="text-size-16 text-base-60 font-semibold">{{ t('esgDashboard.impact.carReductionEffect') }}</p>
            <div class="w-[1px] h-4 bg-base-40" />
            <p class="text-size-24 text-info-80 font-bold flex items-center gap-x-4">
              <img src="/images/car.svg" alt="" />
              <span>{{ t('esgDashboard.impact.cars', { count: '873' }) }}</span>
            </p>
          </div>
        </div>

        <div>
          <p class="flex items-center gap-x-1 text-size-14 text-positive-80 font-semibold mb-2">
            <Info class="w-4 h-4" />
            <span>{{ t('esgDashboard.impact.impactCriteria') }}</span>
          </p>
          <ul class="text-size-14 text-base-80 list-disc pl-5">
            <li>{{ t('esgDashboard.impact.co2Reduction') }}: {{ t('esgDashboard.impact.co2ReductionDesc') }}</li>
            <li>{{ t('esgDashboard.impact.waterSaving') }}: {{ t('esgDashboard.impact.waterSavingDesc') }}</li>
            <li>{{ t('esgDashboard.impact.greeningEffect') }}/{{ t('esgDashboard.impact.carReductionEffect') }}: {{ t('esgDashboard.impact.greeningCarDesc') }}</li>
          </ul>
        </div>
      </section>

      <section class="mb-16">
        <h3 class="text-size-24 font-bold mb-1">{{ t('esgDashboard.wasteCollection.title', { date: reportDate }) }}</h3>
        <p class="text-base-70 mb-4">{{ t('esgDashboard.wasteCollection.description') }}</p>

        <div class="flex items-center justify-center bg-base-40 text-size-32 text-base-10 font-bold min-h-[540px]">
          {{ t('esgDashboard.wasteCollection.dataArea') }}
        </div>
      </section>

      <section>
        <h3 class="text-size-24 font-bold mb-1">{{ t('esgDashboard.yoyAnalysis.title', { date: reportDate }) }}</h3>
        <p class="text-base-70 mb-4">{{ t('esgDashboard.yoyAnalysis.description') }}</p>

        <div class="flex items-center justify-center bg-base-40 text-size-32 text-base-10 font-bold min-h-[540px]">
          {{ t('esgDashboard.yoyAnalysis.dataArea') }}
        </div>
      </section>
    </Card>
  </div>
</template>

<style scoped lang="scss">

</style>