<script setup lang="ts">
import {computed, ref} from 'vue'
import {Calendar, ChevronRight, CreditCard, Crown, Mail, User} from 'lucide-vue-next'
import {useAuthStore} from '@/stores/auth.ts'
import {useRouter} from 'vue-router'
import BaseInput from '@/components/base/BaseInput.vue'
import BasePage from "@/components/BasePage.vue";
import {APP_NAME, GITHUB} from "@/config/env.ts";
import BaseButton from "@/components/BaseButton.vue";

const authStore = useAuthStore()
const router = useRouter()

// Check login state
const isLoggedIn = computed(() => authStore.isLogin)

// Form data
const username = ref('Brian W')
const email = ref('ttentau@gmail.com')
const receiveNotifications = ref(false)

// Mock subscription data (you can replace with real data from your API)
const subscriptionData = ref({
  plan: 'Premium',
  status: 'active',
  expiresAt: '2025-12-31',
  autoRenew: true,
  paymentMethod: '信用卡 ****1234'
})

// UI state
const isEditingUsername = ref(false)
const isEditingEmail = ref(false)
const showPasswordSection = ref(false)

// Handlers
const handleLogin = () => {
  router.push('/login')
}

const handleLogout = () => {
  authStore.logout()
  router.push('/login')
}

const editUsername = () => {
  isEditingUsername.value = true
}

const saveUsername = () => {
  isEditingUsername.value = false
  // Here you would typically save to backend
}

const editEmail = () => {
  isEditingEmail.value = true
}

const saveEmail = () => {
  isEditingEmail.value = false
  // Here you would typically save to backend
}

const toggleNotifications = () => {
  receiveNotifications.value = !receiveNotifications.value
}

const downloadPersonalInfo = () => {
  console.log('Download personal info')
}

const deleteAccount = () => {
  if (confirm('确定要删除您的账户吗？此操作无法撤销。')) {
    console.log('Delete account')
  }
}

const contactSupport = () => {
  console.log('Contact support')
}

const leaveTrustpilotReview = () => {
  window.open(GITHUB + '/issues', '_blank')
}
</script>

<template>
  <BasePage>
    <!-- Unauthenticated View -->
    <div v-if="!isLoggedIn" class="w-full max-w-md">
      <div class="bg-white rounded-2xl shadow-lg p-8 text-center">
        <div class="mb-8">
          <div class="w-20 h-20 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <User class="w-10 h-10 text-blue-600"/>
          </div>
          <h1 class="text-2xl font-bold text-gray-900 mb-2">欢迎使用</h1>
          <p class="text-gray-600">请登录以管理您的账户</p>
        </div>

        <button
          @click="handleLogin"
          class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 px-6 rounded-xl transition-colors duration-200 mb-4"
        >
          登录
        </button>

        <p class="text-sm text-gray-500">
          还没有账户？
          <a href="#" class="text-blue-600 hover:text-blue-700 font-medium">立即注册</a>
        </p>
      </div>
    </div>

    <!-- Authenticated View -->
    <div v-else class="w-full max-w-4xl">
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <!-- Main Account Settings -->
        <div class="lg:col-span-2">
          <div class="card">
            <!-- Header -->
            <div class="px-6 border-b border-gray-200">
              <h1 class="text-xl font-bold text-gray-900">帐户</h1>
            </div>

            <!-- Username Section -->
            <div class="px-6 py-4 flex items-center justify-between hover:bg-gray-50 transition-colors">
              <div class="flex-1">
                <div class="text-sm font-medium text-gray-700 mb-1">用户名</div>
                <div class="flex items-center gap-3">
                  <User class="w-4 h-4 text-gray-500"/>
                  <BaseInput
                    v-if="isEditingUsername"
                    v-model="username"
                    type="text"
                    size="normal"
                    @blur="saveUsername"
                    @keyup.enter="saveUsername"
                    class="flex-1 max-w-xs"
                    autofocus
                  />
                  <span v-else class="text-gray-900">{{ username }}</span>
                </div>
              </div>

              <IconFluentTextEditStyle20Regular
                @click="isEditingUsername ? saveUsername() : editUsername()"
                class="text-xl"/>
            </div>
            <div class="border-t border-gray-200"></div>

            <!-- Email Section -->
            <div class="px-6 py-4 flex items-center justify-between hover:bg-gray-50 transition-colors">
              <div class="flex-1">
                <div class="text-sm font-medium text-gray-700 mb-1">电子邮箱</div>
                <div class="flex items-center gap-3">
                  <Mail class="w-4 h-4 text-gray-500"/>
                  <BaseInput
                    v-if="isEditingEmail"
                    v-model="email"
                    type="email"
                    size="normal"
                    @blur="saveEmail"
                    @keyup.enter="saveEmail"
                    class="flex-1 max-w-xs"
                    autofocus
                  />
                  <span v-else class="text-gray-900">{{ email }}</span>
                </div>
              </div>
              <IconFluentTextEditStyle20Regular
                @click="isEditingEmail ? saveEmail() : editEmail()"
                class="text-xl"/>
            </div>

            <div class="border-t border-gray-200"></div>

            <!-- Password Section -->
            <div class="px-6 py-4 flex items-center justify-between hover:bg-gray-50 transition-colors">
              <div class="flex-1">
                <div class="text-sm font-medium text-gray-700 mb-1">设置密码</div>
                <div class="text-sm text-gray-500">在此输入密码</div>
              </div>
              <IconFluentChevronLeft28Filled @click="showPasswordSection = !showPasswordSection"
                                             class="transition-transform"
                                             :class="['rotate-270','rotate-180'][showPasswordSection?0:1]"/>
            </div>
            <div class="border-t border-gray-200"></div>

            <!-- Notification Toggle -->
            <div class="px-6 py-4 flex items-center justify-between hover:bg-gray-50 transition-colors">
              <div class="flex-1">
                <div class="text-sm font-medium text-gray-700 mb-1">同意接收优惠信息</div>
                <div class="text-sm text-gray-500">第一时间掌握 Lingvist 的各种优惠及最新消息。</div>
              </div>
              <button
                @click="toggleNotifications"
                class="relative inline-flex h-6 w-11 items-center rounded-full transition-colors"
                :class="receiveNotifications ? 'bg-blue-600' : 'bg-gray-200'"
              >
                <span
                  class="inline-block h-4 w-4 transform rounded-full bg-white transition-transform"
                  :class="receiveNotifications ? 'translate-x-6' : 'translate-x-1'"
                />
              </button>
            </div>
            <div class="border-t border-gray-200"></div>


            <!-- Contact Support -->
            <div class="px-6 py-4 flex items-center justify-between hover:bg-gray-50 transition-colors cursor-pointer"
                 @click="contactSupport">
              <div class="flex-1">
                <div class="text-sm font-medium text-gray-700 mb-1">联系{{ APP_NAME }}客服</div>
              </div>
              <ChevronRight class="w-5 h-5 text-gray-400"/>
            </div>
            <div class="border-t border-gray-200"></div>

            <!-- Trustpilot Review -->
            <div class="px-6 py-4 flex items-center justify-between hover:bg-gray-50 transition-colors cursor-pointer"
                 @click="leaveTrustpilotReview">
              <div class="flex-1">
                <div class="text-sm font-medium text-gray-700 mb-1">在 {{ APP_NAME }} 上留下评论</div>
              </div>
              <ChevronRight class="w-5 h-5 text-gray-400"/>
            </div>

            <!-- Logout Button -->
            <div class="px-6 py-6 border-t border-gray-200">
              <button
                @click="handleLogout"
                class="w-full bg-gray-800 hover:bg-gray-900 text-white font-semibold py-3 px-6 rounded-xl transition-colors duration-200"
              >
                登出
              </button>
            </div>

            <!-- Footer Links -->
            <div class="px-6 py-4 border-t border-gray-200 text-center">
              <div class="text-sm text-gray-500">
                <a href="/user-agreement.html" class="text-gray-500 hover:text-gray-700 underline">用户协议</a>
                、
                <a href="/privacy-policy.html" class="text-gray-500 hover:text-gray-700 underline">隐私政策</a>
              </div>
            </div>
          </div>
        </div>

        <!-- Subscription Information -->
        <div class="lg:col-span-1">
          <div class="card">
            <div class="flex items-center gap-3 mb-4">
              <Crown class="w-6 h-6 text-yellow-500"/>
              <h2 class="text-lg font-bold text-gray-900">订阅信息</h2>
            </div>

            <div class="space-y-4">
              <div>
                <div class="text-sm text-gray-500 mb-1">当前计划</div>
                <div class="text-lg font-semibold text-gray-900">{{ subscriptionData.plan }}</div>
              </div>

              <div>
                <div class="text-sm text-gray-500 mb-1">状态</div>
                <div class="flex items-center gap-2">
                  <div class="w-2 h-2 bg-green-500 rounded-full"></div>
                  <span class="text-sm font-medium text-green-700">{{
                      subscriptionData.status === 'active' ? '活跃' : '已过期'
                    }}</span>
                </div>
              </div>

              <div>
                <div class="text-sm text-gray-500 mb-1">到期时间</div>
                <div class="flex items-center gap-2">
                  <Calendar class="w-4 h-4 text-gray-400"/>
                  <span class="text-sm font-medium text-gray-900">{{ subscriptionData.expiresAt }}</span>
                </div>
              </div>

              <div>
                <div class="text-sm text-gray-500 mb-1">自动续费</div>
                <div class="flex items-center gap-2">
                  <div class="w-2 h-2" :class="subscriptionData.autoRenew ? 'bg-blue-500' : 'bg-gray-400'"
                       rounded-full></div>
                  <span class="text-sm font-medium"
                        :class="subscriptionData.autoRenew ? 'text-blue-700' : 'text-gray-600'">
                    {{ subscriptionData.autoRenew ? '已开启' : '已关闭' }}
                  </span>
                </div>
              </div>

              <div>
                <div class="text-sm text-gray-500 mb-1">付款方式</div>
                <div class="flex items-center gap-2">
                  <CreditCard class="w-4 h-4 text-gray-400"/>
                  <span class="text-sm font-medium text-gray-900">{{ subscriptionData.paymentMethod }}</span>
                </div>
              </div>

              <div class="pt-4 border-t border-gray-200">
                <BaseButton class="w-full">管理订阅</BaseButton>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </BasePage>
</template>