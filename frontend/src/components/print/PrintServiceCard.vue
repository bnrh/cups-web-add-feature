<template>
  <UCard>
    <template #header>
      <div class="flex items-center gap-2 font-semibold">
        <UIcon
          name="i-lucide-badge-dollar-sign"
          class="w-5 h-5 text-primary"
        />
        打印服务
      </div>
    </template>

    <div class="space-y-4">

      <!-- 价格 -->
      <div class="space-y-2 text-sm">

        <div class="flex items-center justify-between">
          <span class="text-muted">黑白打印</span>

          <UBadge color="neutral" variant="soft">
            单面：¥0.12 / 页
          </UBadge>

          <UBadge color="neutral" variant="soft">
            双面：¥0.18 / 页
          </UBadge>
        </div>

        <!-- 彩色打印（已注释） -->
        <!--
        <div class="flex items-center justify-between">
          <span class="text-muted">彩色打印</span>

          <UBadge color="warning" variant="soft">
            ¥1.00 / 页
          </UBadge>
        </div>
        -->

        <div class="flex items-center justify-between">
          <span class="text-muted">HP LaserJet 1020</span>

          <!-- color="error" 字体为红色，color="primary" 字体为绿色  -->
          <!-- <UBadge color="error" variant="soft">  -->
          <UBadge color="primary" variant="soft">
            付费使用
          </UBadge>
        </div>

        <div class="flex items-center justify-between">
          <span class="text-muted">HP Tank 510</span>

          <!-- <UBadge color="primary" variant="soft">  -->
          <UBadge color="error" variant="soft">
            需机子主人同意
          </UBadge>
        </div>

      </div>

      <UDivider />

    <!-- 二维码 -->
    <div class="flex flex-col items-center">
    <div class="flex gap-6">
        <!-- 微信小程序二维码 -->
        <div class="flex flex-col items-center">
        <div class="bg-white rounded-xl p-2 border border-default shadow-sm">
            <img
            src="/Mini_Program_QR_Code.jpg"
            alt="微信小程序二维码"
            class="w-40 h-40 object-contain"
            />
        </div>
        <p class="text-xs text-muted mt-3 text-center">
            微信扫码使用小程序打印
        </p>
        </div>

        <!-- 微信收款二维码 -->
        <div class="flex flex-col items-center">
        <div class="bg-white rounded-xl p-2 border border-default shadow-sm">
            <img
            src="/Business_QR_Code.jpg"
            alt="微信收款二维码"
            class="w-40 h-40 object-contain"
            />
        </div>
        <p class="text-xs text-muted mt-3 text-center">
            微信收款二维码
        </p>
        </div>
    </div>
    </div>

    </div>
  </UCard>
</template>