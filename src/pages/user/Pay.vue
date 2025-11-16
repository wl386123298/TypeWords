<script setup lang="ts">
import { ref } from 'vue'
import BasePage from '@/components/BasePage.vue'
import BaseButton from '@/components/BaseButton.vue'

// Payment method selection
const selectedPaymentMethod = ref('')
const agreeToTerms = ref(false)

// Payment methods - WeChat and Alipay
const paymentMethods = [
  {
    id: 'wechat',
    name: '微信支付',
    icon: '💚',
    description: '使用微信支付'
  },
  {
    id: 'alipay',
    name: '支付宝',
    icon: '💙',
    description: '使用支付宝支付'
  }
]

// Order data (this would typically come from props or store)
const orderData = {
  planName: '月度会员',
  price: 9.99,
  currency: 'US$',
  unit: '每月',
  startDate: new Date().toLocaleDateString('en-US', { 
    year: 'numeric', 
    month: 'long', 
    day: 'numeric' 
  }),
  vatText: '(含增值税)'
}

function selectPaymentMethod(methodId: string) {
  selectedPaymentMethod.value = methodId
}

function handlePayment() {
  if (!selectedPaymentMethod.value) {
    alert('请选择支付方式')
    return
  }
  if (!agreeToTerms.value) {
    alert('请同意服务条款')
    return
  }
  
  // TODO: Implement payment processing
  console.log('Processing payment with:', selectedPaymentMethod.value)
}

function handleChangePlan() {
  // TODO: Navigate back to plan selection
  console.log('Change plan clicked')
}
</script>

<template>
  <BasePage>
    <div class="pay-page min-h-screen py-8">
      <!-- Page Header -->
      <div class="text-center mb-8">
        <h1 class="text-2xl font-semibold text-gray-900 mb-2">安全支付</h1>
        <p class="text-gray-600">选择支付方式完成订单</p>
      </div>

      <!-- Main Content -->
      <div class="max-w-6xl mx-auto px-4">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
          <!-- Left Card: Payment Method Selection -->
          <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
            <h2 class="text-lg font-medium text-gray-900 mb-4">Choose a way to pay</h2>
            
            <div class="space-y-3">
              <div 
                v-for="method in paymentMethods" 
                :key="method.id"
                @click="selectPaymentMethod(method.id)"
                class="flex items-center p-4 border rounded-lg cursor-pointer transition-all duration-200"
                :class="[
                  selectedPaymentMethod === method.id 
                    ? 'border-blue-500 bg-blue-50' 
                    : 'border-gray-200 hover:border-gray-300 hover:bg-gray-50'
                ]"
              >
                <div class="flex items-center flex-1">
                  <span class="text-2xl mr-3">{{ method.icon }}</span>
                  <div>
                    <div class="font-medium text-gray-900">{{ method.name }}</div>
                    <div class="text-sm text-gray-500">{{ method.description }}</div>
                  </div>
                </div>
                <div 
                  class="w-5 h-5 rounded-full border-2 flex items-center justify-center"
                  :class="[
                    selectedPaymentMethod === method.id 
                      ? 'border-blue-500 bg-blue-500' 
                      : 'border-gray-300'
                  ]"
                >
                  <div 
                    v-if="selectedPaymentMethod === method.id"
                    class="w-2 h-2 bg-white rounded-full"
                  ></div>
                </div>
              </div>
            </div>
          </div>

          <!-- Right Card: Order Summary -->
          <div class="bg-white rounded-lg border border-gray-200 shadow-sm p-6">
            <div class="flex items-center justify-between mb-4">
              <h2 class="text-lg font-semibold text-gray-900">订单概要</h2>
              <button 
                @click="handleChangePlan"
                class="px-3 py-1 text-sm text-gray-600 border border-gray-300 rounded-full hover:bg-gray-50 transition-colors"
              >
                更改
              </button>
            </div>

            <!-- Plan Info -->
            <div class="mb-4">
              <div class="text-purple-600 text-sm mb-2">付费方案（月费）订阅</div>
              <div class="text-gray-900 mb-4">
                从 {{ orderData.startDate }} 开始:
              </div>
            </div>

            <!-- Price -->
            <div class="flex items-baseline mb-4">
              <span class="text-3xl font-semibold text-gray-900">{{ orderData.currency }}{{ orderData.price }}</span>
              <span class="text-gray-600 ml-2">/ {{ orderData.unit }}</span>
            </div>
            <div class="text-sm text-gray-500 mb-6">{{ orderData.vatText }}</div>

            <!-- Info Box -->
            <div class="bg-gray-50 rounded-lg p-4 mb-6">
              <p class="text-sm text-gray-600 mb-2">
                你将于 {{ orderData.startDate }} 付费。
              </p>
              <p class="text-sm text-gray-600">
                在试订期间和订阅开始前的24小时内，你可随时通过 "账户" > "订阅" 页面取消或改订。
              </p>
            </div>

            <!-- Terms Checkbox -->
            <div class="flex items-start mb-6">
              <input 
                type="checkbox" 
                id="terms"
                v-model="agreeToTerms"
                class="mt-1 w-4 h-4 text-blue-600 border-gray-300 rounded focus:ring-blue-500"
              >
              <label for="terms" class="ml-3 text-sm text-gray-700">
                我同意 Lingvist 的 
                <a href="#" class="text-purple-600 hover:text-purple-700 underline">服务条款</a>
              </label>
            </div>

            <!-- Payment Button -->
            <BaseButton 
              class="w-full"
              size="large"
              :type="selectedPaymentMethod && agreeToTerms ? 'primary' : 'default'"
              :disabled="!selectedPaymentMethod || !agreeToTerms"
              @click="handlePayment"
            >
              选择
            </BaseButton>
          </div>
        </div>
      </div>
    </div>
  </BasePage>
</template>

<style scoped lang="scss">
.pay-page {
  @apply min-h-screen;
}

/* Custom radio button style */
.payment-method {
  @apply flex items-center p-4 border rounded-lg cursor-pointer transition-all duration-200;
  
  &:hover {
    @apply border-gray-300 bg-gray-50;
  }
  
  &.selected {
    @apply border-blue-500 bg-blue-50;
  }
}

.payment-radio {
  @apply w-5 h-5 rounded-full border-2 flex items-center justify-center;
  
  &.selected {
    @apply border-blue-500 bg-blue-500;
  }
  
  &.unselected {
    @apply border-gray-300;
  }
}

.radio-dot {
  @apply w-2 h-2 bg-white rounded-full;
}
</style>