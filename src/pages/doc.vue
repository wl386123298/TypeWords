<script setup lang="ts">
import { computed, ref } from 'vue'
import BasePage from '@/components/BasePage.vue'
import BaseButton from '@/components/BaseButton.vue'

// 类型定义
interface Resource {
  name: string
  description?: string
  difficulty?: string
  link: string
  author?: string
  features?: string
  suitable?: string
}

interface Subcategory {
  name: string
  description?: string
  resources: Resource[]
}

interface Category {
  id: string
  name: string
  icon: string
  description?: string
  resources?: Resource[]
  subcategories?: Subcategory[]
}

// 资源分类
const categories = ref<Category[]>([
  {
    id: 'new-concept',
    name: '新概念英语',
    icon: '📚',
    description: '经典英语教材，适合系统学习',
    resources: [
      {
        name: '新概念英语第一册',
        description: '适合英语初学者',
        difficulty: '入门',
        link: 'https://pan.quark.cn/s/92a317cf1a16',
      },
      {
        name: '新概念英语第二册',
        description: '基础英语学习，巩固语法和词汇',
        difficulty: '基础',
        link: 'https://pan.quark.cn/s/1ee9c8a7e8e2',
      },
      {
        name: '新概念英语第三册',
        description: '提高英语水平，增强阅读能力',
        difficulty: '进阶',
        link: 'https://pan.quark.cn/s/b35c2859812a',
      },
      {
        name: '新概念英语第四册',
        description: '高级英语学习，提升综合能力',
        difficulty: '高级',
        link: 'https://pan.quark.cn/s/a56713cafbc5',
      },
      {
        name: '新概念英青少年版',
        description: '儿童读物',
        difficulty: '7岁至14岁',
        link: 'https://pan.quark.cn/s/9de8d7967de2',
      },
      {
        name: '新概念英语1-4 教材高清 PDF',
        description: '仅 1-4 册的教材高清扫描版 PDF',
        difficulty: '',
        link: 'https://pan.quark.cn/s/ec49145d6b00',
      },
      {
        name: '新概念讲解视频',
        description: '多家机构/个人的讲解视频',
        difficulty: '',
        link: 'https://pan.quark.cn/s/09e98acd55b4',
      },
      {
        name: '新概念合集',
        description: '包含前面的内容',
        difficulty: '',
        link: 'https://pan.quark.cn/s/667e2e48eba4',
      },
    ],
  },
  {
    id: 'exam',
    name: '电视/电影',
    icon: '🎯',
    description: '一些不错的美/英剧，可练听力和口语',
    resources: [
      {
        name: '老友记',
        description: '',
        difficulty: '喜剧/爱情',
        link: 'https://pan.quark.cn/s/674834e7a5b1',
      },
      {
        name: '生活大爆炸',
        description: '',
        difficulty: '喜剧/爱情',
        link: 'https://pan.quark.cn/s/0539c10704ba',
      },
      {
        name: '是大臣/是首相',
        description: '',
        difficulty: '喜剧/讽刺',
        link: 'https://pan.quark.cn/s/316323ce51d5',
      },
      {
        name: '破产姐妹',
        description: '',
        difficulty: '喜剧',
        link: 'https://pan.quark.cn/s/40af6faaa19a',
      },
      {
        name: '绝望主妇',
        description: '',
        difficulty: '悬疑',
        link: 'https://pan.quark.cn/s/bcccdf9e788b',
      },
      {
        name: '纸牌屋',
        description: '',
        difficulty: '纸牌屋',
        link: 'https://pan.quark.cn/s/d2f3082508fd',
      },
      {
        name: '电视/电影合集',
        description: '包含前面的内容',
        difficulty: '',
        link: 'https://pan.quark.cn/s/84ecb30b700b',
      },
    ],
  },
  {
    id: 'grammar',
    name: '语法学习',
    icon: '📝',
    description: '',
    subcategories: [
      {
        name: '经典教材',
        description: '',
        resources: [
          {
            name: '英语语法新思维',
            author: '张满胜',
            features:'从思维角度讲解语法，注重理解而非死记硬背，分为初级、中级、高级三册，循序渐进',
            suitable:'希望系统建立语法体系的学习者',
            difficulty: '',
            link: 'https://pan.quark.cn/s/d06abef6c737',
          },
          {
            name: '薄冰英语语法',
            author: '薄冰',
            features:'老牌经典,体系完整,分类非常细,查语法点方便',
            suitable:'中学生或基础较弱的学习者',
            difficulty: '',
            link: 'https://pan.quark.cn/s/30777ceba5b9',
          },
          {
            name: '实用英语语法',
            author: '张道真',
            features:'国内经典语法教材，内容详实全面，例句丰富，适合作为工具书查阅',
            suitable:'需要权威参考书的学生或教师',
            difficulty: '',
            link: 'https://pan.baidu.com/s/xxx',
          },
          {
            name: '旋元估文法',
            author: '旋元估',
            features:'以通俗易懂的语言解析复杂语法，强调“理解逻辑”，适合突破语法难点',
            suitable:'对传统语法教学感到枯燥，想轻松掌握核心逻辑的学习者',
            difficulty: '繁体中文版',
            link: 'https://pan.quark.cn/s/0d0de559794e',
          },
        ],
      },
      {
        name: '进阶提升',
        description: '',
        resources: [
          {
            name: '剑桥英语语法(English Grammar in Use)',
            author: '剑桥大学出版',
            features:'分为初级、中级、高级三册，经典畅销语法自学书，解释简明且有大量练习',
            suitable:'需要结合国际考试的学习者',
            description: '',
            difficulty: '中文版',
            link: 'https://pan.quark.cn/s/d4a6ef53c04d',
          },
          {
            name: 'Oxford English Grammar(牛津英语语法)',
            author: 'Sidney Greenbaum & Gerald Nelson',
            features:'分为基础、提升、高级三册，英式语法权威，解释清晰、例句地道，适合备考雅思/托福',
            suitable:'想全面系统梳理语法体系的人',
            difficulty: '英文版',
            link: 'https://pan.quark.cn/s/ca505875e68c',
          },
          {
            name: '实用英语用法(Practical English Usage)',
            author: 'Michael Swan',
            features:'解释非常细致，尤其适合纠正常见错误和困惑',
            suitable:'中高级学习者，适合作为语法问题的工具书',
            difficulty: '中文版/英文版',
            link: 'https://pan.quark.cn/s/05006e705a77',
          },
        ],
      },
    ],
  },
  {
    id: 'listening',
    name: '听力训练',
    icon: '🎧',
    description: '提升英语听力水平',
    resources: [
      {
        name: 'VOA慢速英语合集',
        description: '新闻类听力材料，语速适中，内容丰富',
        difficulty: '初级',
        link: 'https://pan.quark.cn/s/23fc83043ca4',
      },
      // {
      //   name: 'BBC Learning English',
      //   description: 'BBC官方英语学习资源，涵盖多方面内容',
      //   difficulty: '中高级',
      //   link: 'https://pan.baidu.com/s/xxx',
      // },
      {
        name: 'TED-ED 科普动画',
        description: 'TED-Ed 是一个专为初高中生所设计的在3到5分钟长的科普动画課程',
        difficulty: '初级',
        link: 'https://pan.quark.cn/s/e4c0182833ba',
      },
      {
        name: '哈弗演讲',
        description: '高质量演讲，锻炼听力同时开拓视野',
        difficulty: '中高级',
        link: 'https://pan.quark.cn/s/f2bfa8a50d25',
      },
    ],
  },
])

// 当前选中的分类
const selectedCategory = ref('all')

// 筛选后的资源
const filteredResources = computed(() => {
  if (selectedCategory.value === 'all') {
    return categories.value
  }
  return categories.value.filter(cat => cat.id === selectedCategory.value)
})

// 跳转到网盘链接
const openLink = (url: string) => {
  window.open(url, '_blank')
}

// 根据难度获取对应的样式类
const getDifficultyClass = (difficulty: string) => {
  switch (difficulty) {
    case '入门':
      return 'bg-green-500'
    case '基础':
      return 'bg-blue-500'
    case '中级':
      return 'bg-purple-500'
    case '进阶':
      return 'bg-amber-500'
    case '高级':
      return 'bg-red-500'
    case '全级别':
      return 'bg-gray-500'
    default:
      return 'bg-blue-500'
  }
}
</script>

<template>
  <BasePage>
    <div class="flex flex-col items-center justify-center px-4 py-8">
      <!-- 页面标题 -->
      <div class="text-center mb-8">
        <h1 class="text-4xl font-bold mb-4">📚 英语学习资源分享</h1>
        <p class="text-lg text-gray-600 dark:text-gray-300 max-w-3xl mx-auto">
          以下是我整理的个人收藏的优质英语学习资源，希望对大家有所帮助！
        </p>
      </div>

      <!-- 分类筛选 -->
      <div
        class="flex flex-wrap justify-center gap-2 mb-8 p-4 bg-white dark:bg-gray-800 rounded-lg shadow-md"
      >
        <BaseButton
          :type="selectedCategory === 'all' ? 'primary' : 'info'"
          @click="selectedCategory = 'all'"
        >
          全部资源
        </BaseButton>
        <BaseButton
          v-for="category in categories"
          :key="category.id"
          :type="selectedCategory === category.id ? 'primary' : 'info'"
          @click="selectedCategory = category.id"
        >
          {{ category.icon }} {{ category.name }}
        </BaseButton>
      </div>

      <!-- 资源列表 -->
      <div class="w-full">
        <div v-for="category in filteredResources" :key="category.id" class="mb-12">
          <div class="text-center mb-6">
            <h2 class="text-2xl font-bold mb-2">{{ category.icon }} {{ category.name }}</h2>
            <p v-if="category.description" class="text-gray-600 dark:text-gray-300">
              {{ category.description }}
            </p>
          </div>

          <!-- 如果有子分类，显示子分类 -->
          <template v-if="category.subcategories">
            <div
              v-for="subcategory in category.subcategories"
              :key="subcategory.name"
              class="mb-10"
            >
              <div class="text-center mb-4">
                <h3 class="text-xl font-semibold mb-2 text-gray-800 dark:text-gray-200">
                  {{ subcategory.name }}
                </h3>
                <p v-if="subcategory.description" class="text-gray-600 dark:text-gray-300">
                  {{ subcategory.description }}
                </p>
              </div>

              <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
                <div
                  v-for="resource in subcategory.resources"
                  :key="resource.name"
                  class="card-white min-h-45 mb-0 hover:shadow-xl transition-all duration-300 hover:-translate-y-1 flex flex-col justify-between"
                >
                  <div class="">
                    <div class="text-xl font-semibold mb-3 text-gray-800 dark:text-gray-100">
                      {{ resource.name }}
                    </div>
                    <div class="space-y-2 mb-4">
                      <p v-if="resource.author" class="text-sm text-gray-600 dark:text-gray-300">
                        <span class="font-medium">📍 作者：</span>{{ resource.author }}
                      </p>
                      <p v-if="resource.features" class="text-sm text-gray-600 dark:text-gray-300">
                        <span class="font-medium">🌟 特点：</span>{{ resource.features }}
                      </p>
                      <p v-if="resource.suitable" class="text-sm text-gray-600 dark:text-gray-300">
                        <span class="font-medium">📌 适合：</span>{{ resource.suitable }}
                      </p>
                      <p v-if="resource.description" class="text-sm text-gray-600 dark:text-gray-300">
                        {{ resource.description }}
                      </p>
                      <span
                        v-if="resource.difficulty"
                        class="inline-block px-3 py-1 rounded-full text-xs font-medium text-white"
                        :class="getDifficultyClass(resource.difficulty)"
                      >
                        {{ resource.difficulty }}
                      </span>
                    </div>
                  </div>
                  <div class="flex flex-col gap-3">
                    <BaseButton type="primary" @click="openLink(resource.link)">
                      打开链接
                    </BaseButton>
                  </div>
                </div>
              </div>
            </div>
          </template>

          <!-- 如果没有子分类，直接显示资源 -->
          <template v-else>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
              <div
                v-for="resource in category.resources"
                :key="resource.name"
                class="card-white min-h-45 mb-0 hover:shadow-xl transition-all duration-300 hover:-translate-y-1 flex flex-col justify-between"
              >
                <div class="">
                  <div class="text-xl font-semibold mb-3 text-gray-800 dark:text-gray-100">
                    {{ resource.name }}
                  </div>
                  <div class="space-y-2 mb-4">
                    <p v-if="resource.author" class="text-sm text-gray-600 dark:text-gray-300">
                      <span class="font-medium">📍 作者：</span>{{ resource.author }}
                    </p>
                    <p v-if="resource.features" class="text-sm text-gray-600 dark:text-gray-300">
                      <span class="font-medium">🌟 特点：</span>{{ resource.features }}
                    </p>
                    <p v-if="resource.suitable" class="text-sm text-gray-600 dark:text-gray-300">
                      <span class="font-medium">📌 适合：</span>{{ resource.suitable }}
                    </p>
                    <p v-if="resource.description" class="text-sm text-gray-600 dark:text-gray-300">
                      {{ resource.description }}
                    </p>
                    <span
                      v-if="resource.difficulty"
                      class="inline-block px-3 py-1 rounded-full text-xs font-medium text-white"
                      :class="getDifficultyClass(resource.difficulty)"
                    >
                      {{ resource.difficulty }}
                    </span>
                  </div>
                </div>
                <div class="flex flex-col gap-3">
                  <BaseButton type="primary" @click="openLink(resource.link)"> 打开链接 </BaseButton>
                </div>
              </div>
            </div>
          </template>
        </div>
      </div>

      <!-- 页面底部 -->
      <div class="mt-12 pt-8 border-t border-gray-200 dark:border-gray-700">
        <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6">
          <h3 class="text-xl font-bold mb-4">💡 温馨提示</h3>
          <ul class="list-disc list-inside space-y-2 text-gray-600 dark:text-gray-300">
            <li>所有资源均来自互联网收集，仅供学习交流使用</li>
            <li>如果链接失效，请及时<a :href="`https://v.wjx.cn/vm/ev0W7fv.aspx#`"
                                       target="_blank">告知</a>，我会尽快更新</li>
          </ul>
        </div>
      </div>
    </div>
  </BasePage>
</template>
