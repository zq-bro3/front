<template>
  <div class="flex min-h-screen bg-white">
    <aside class="w-60 bg-[#f4f8fc] flex flex-col">
      <div class="p-6">
        <img class="w-[130px] h-[22px]" alt="Frame" src="/frame.svg" />
      </div>

      <nav class="flex-1 px-3">
        <div
          v-for="(item, index) in sidebarMenuItems"
          :key="index"
          :class="[
            'flex items-center gap-3 px-3 py-3 mb-1 rounded-md cursor-pointer',
            item.active ? 'bg-[#e6ecff]' : '',
          ]"
        >
          <img
            class="w-6 h-6 object-contain"
            :alt="item.label"
            :src="item.icon"
          />
          <span
            class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#434d6d] text-base font-normal"
          >
            {{ item.label }}
          </span>
        </div>
      </nav>

      <div class="p-6 border-t border-[#434d6d]/20">
        <div
          class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] font-normal text-[#434d6d] text-base"
        >
          13892910930
        </div>
      </div>
    </aside>

    <main class="flex-1 flex flex-col">
      <header
        class="h-20 border-b border-transparent flex items-center px-6"
      >
        <div
          class="w-[109px] h-[45px] bg-white rounded-[7px] shadow-[7px_4px_10.9px_#d8ecff66] flex items-center justify-center gap-2 cursor-pointer"
        >
          <span
            class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#292f41] text-[15px] font-normal"
          >
            立项会
          </span>
          <ChevronDownIcon class="w-3 h-3 text-[#292f41]" />
        </div>
      </header>

      <div class="flex-1 flex">
        <div class="w-48 border-r border-gray-200 p-6">
          <div class="space-y-4">
            <div
              v-for="type in meetingTypes"
              :key="type.value"
              :class="[
                'py-3 px-4 rounded-md cursor-pointer',
                selectedMeetingType === type.value
                  ? 'border-2 border-[#e6edff]'
                  : '',
              ]"
              @click="selectedMeetingType = type.value"
            >
              <span
                class="[font-family:'Dream_Han_Sans_CN-W16',Helvetica] text-[#434d6d] text-base font-normal"
              >
                {{ type.label }}
              </span>
            </div>
          </div>
        </div>

        <div class="flex-1 p-6">
          <div class="flex items-center justify-between mb-8">
            <Button
              class="bg-[#003df7] hover:bg-[#003df7]/90 rounded-[40px] h-10 px-6"
            >
              <span
                class="[font-family:'Dream_Han_Sans_CN-W16',Helvetica] text-white text-[15px] font-normal"
              >
                开始会议
              </span>
            </Button>
          </div>

          <h1
            class="[font-family:'Dream_Han_Sans_CN-W20',Helvetica] text-black text-xl font-normal mb-6"
          >
            立项会
          </h1>

          <div class="relative w-[284px] mb-8">
            <Input
              placeholder="会议关键字"
              class="h-[29px] rounded-[62px] border-[#e9e9eb] pl-4 pr-10 [font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#9b9999] text-base"
            />
            <SearchIcon
              class="absolute right-3 top-1/2 -translate-y-1/2 w-5 h-5 text-[#9b9999]"
            />
          </div>

          <div class="flex items-center justify-between mb-6">
            <div class="flex gap-4">
              <div
                class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#868fab] text-base font-normal"
              >
                会议名称
              </div>
            </div>
            <div class="flex items-center gap-12">
              <div
                class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#868fab] text-base font-normal"
              >
                会议时间
              </div>
              <div class="flex items-center gap-4">
                <div
                  class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#868fab] text-base font-normal"
                >
                  操作
                </div>
                <div class="flex gap-2">
                  <Button
                    variant="outline"
                    class="h-[29px] rounded-[46px] border-[#003df7] px-4"
                  >
                    <CheckCircle2Icon
                      class="w-[18px] h-5 text-[#003df7] mr-1"
                    />
                    <span
                      class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#003df7] text-base font-normal"
                    >
                      选择
                    </span>
                  </Button>
                  <Button
                    variant="outline"
                    class="h-[29px] rounded-[58px] border-[#7a84a3] px-4"
                  >
                    <Trash2Icon class="w-[18px] h-5 text-[#7a84a3] mr-1" />
                    <span
                      class="[font-family:'Dream_Han_Sans_CN-W13',Helvetica] text-[#7a84a3] text-base font-normal"
                    >
                      删除
                    </span>
                  </Button>
                </div>
              </div>
            </div>
          </div>

          <div class="space-y-0">
            <template v-for="(meeting, index) in meetingData" :key="meeting.id">
              <div class="flex items-center justify-between py-5">
                <div
                  class="flex-1 [font-family:'Dream_Han_Sans_CN-W16',Helvetica] text-[#434d6d] text-base font-normal"
                >
                  {{ meeting.name }}
                </div>
                <div class="flex items-center gap-12">
                  <div
                    class="w-[84px] [font-family:'Dream_Han_Sans_CN-W16',Helvetica] text-[#434d6d] text-base font-normal"
                  >
                    {{ meeting.date }}
                  </div>
                  <div class="flex items-center gap-4">
                    <img
                      class="w-[15px] h-[19px] cursor-pointer"
                      alt="Edit"
                      :src="meeting.editIcon"
                    />
                    <img
                      class="w-[21px] h-[15px] cursor-pointer"
                      alt="Upload"
                      :src="meeting.uploadIcon"
                    />
                  </div>
                </div>
              </div>
              <div
                v-if="index < meetingData.length - 1"
                class="h-px bg-gray-200"
              />
            </template>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import {
  CheckCircle2Icon,
  ChevronDownIcon,
  SearchIcon,
  Trash2Icon,
} from "lucide-vue-next";
import { ref } from "vue";
import Button from "../../components/ui/Button.vue";
import Input from "../../components/ui/Input.vue";

const sidebarMenuItems = [
  {
    icon: "/vector.svg",
    label: "首页",
  },
  {
    icon: "/----icon.png",
    label: "项目尽调",
  },
  {
    icon: "/vector-1.svg",
    label: "报告生成",
  },
  {
    icon: "/group-34.png",
    label: "行业研究",
  },
  {
    icon: "/-----1.svg",
    label: "流程会议",
    active: true,
  },
  {
    icon: "/group-258.png",
    label: "项目管理",
  },
  {
    icon: "/folder-open-03.svg",
    label: "投后管理",
  },
  {
    icon: "/group-260.png",
    label: "回收站",
  },
];

const meetingTypes = [
  { value: "立项会", label: "立项会" },
  { value: "风控会", label: "风控会" },
  { value: "投决会", label: "投决会" },
  { value: "其他会议", label: "其他会议" },
];

const meetingData = [
  {
    id: 1,
    name: "立项会议名称会议名称会议名称会议名称1",
    date: "2025-10-11",
    editIcon: "/group-102.png",
    uploadIcon: "/group-103.png",
  },
  {
    id: 2,
    name: "立项会议名称会议名称会议名称会议名称会议名称2",
    date: "2025-08-13",
    editIcon: "/group-104.png",
    uploadIcon: "/group-105.png",
  },
  {
    id: 3,
    name: "立项会议名称会议名称会议名称会议名称3",
    date: "2025-05-27",
    editIcon: "/group-106.png",
    uploadIcon: "/group-107.png",
  },
  {
    id: 4,
    name: "立项会议名称会议名称会议名称会议名称会议名称会议名称4",
    date: "2025-05-12",
    editIcon: "/group-108.png",
    uploadIcon: "/group-109.png",
  },
  {
    id: 5,
    name: "立项会议名称会议名称会议名称会议名称5",
    date: "2025-04-22",
    editIcon: "/group-110.png",
    uploadIcon: "/group-111.png",
  },
  {
    id: 6,
    name: "立项会议名称会议名称会议名称会议名称会议名称6",
    date: "2025-04-09",
    editIcon: "/group-112.png",
    uploadIcon: "/group-113.png",
  },
];

const selectedMeetingType = ref("立项会");
</script>
