<template>

  <!-- 公告弹窗 -->
  <div
    v-if="showNotice"
    class="fixed inset-0 z-50 flex items-center justify-center bg-black/50"
  >
    <div class="bg-white rounded-2xl shadow-xl p-6 w-[90%] max-w-md">
      <h2 class="text-xl font-bold mb-4">
        系统公告
      </h2>

      <div class="text-gray-700 space-y-2">
        <p>禁止打印违法违规内容。</p>
        <p>使用 HP LaserJet 1020 打印需要付费。</p>
        <p>页数可查看打印记录显示。</p>
        <p>使用 HP Tank 510 打印需要询问叶同学同意。</p>
        <p>微信小程序和网页端都可以直接打印。</p>
        <p>网页端登录用户名：share 密码：share</p>
      </div>

      <div class="mt-6 text-right">
        <button
          class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600"
          @click="closeNotice"
        >
          我知道了
        </button>
      </div>
    </div>
  </div>

  <div class="flex items-center justify-center h-full p-3 sm:p-4 md:p-6">
    <UCard class="w-full max-w-md shadow-lg">
      <template #header>
        <h2 class="text-xl font-bold flex items-center gap-2">
          <UIcon name="i-lucide-user" class="w-5 h-5" />
          登录
        </h2>
      </template>
      
      <!-- 错误提示 -->
      <UAlert
        v-if="error"
        icon="i-lucide-triangle-alert"
        color="error"
        variant="soft"
        :title="error"
        class="mb-6"
      />
      
      <UForm @submit="login" :state="state" class="space-y-6">
        <UFormField label="用户名" name="username" required>
          <UInput v-model="state.username" icon="i-lucide-user" size="lg" class="w-full" />
        </UFormField>
        <UFormField label="密码" name="password" required>
          <UInput v-model="state.password" type="password" icon="i-lucide-lock" size="lg" class="w-full" />
        </UFormField>
        
        <div class="mt-6">
          <UButton 
            type="submit" 
            color="primary" 
            icon="i-lucide-log-in" 
            size="lg"
            class="w-full"
            :loading="loading"
          >
            登录
          </UButton>
        </div>
      </UForm>
    </UCard>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'

const state = reactive({
  username: '',
  password: ''
})
const error = ref('')
const loading = ref(false)

const emit = defineEmits(['login-success'])

// ─── 公告弹窗 ───────────────────────────────────────────────
const showNotice = ref(true)

function closeNotice() {
  showNotice.value = false

  // localStorage.setItem("print_notice_read", "1")
}

// onMounted(async () => {
// 
//   const readed = localStorage.getItem("print_notice_read")
// 
//   if (readed === "1") {
//     showNotice.value = false
//   }
// 
//   await refreshAll()
// })

async function login() {
  error.value = ''
  loading.value = true
  try {
    const resp = await fetch('/api/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ username: state.username, password: state.password }),
      credentials: 'include'
    })
    if (!resp.ok) {
      try {
        const data = await resp.json()
        error.value = data.error || data.message || '用户名或密码错误'
      } catch {
        error.value = '用户名或密码错误'
      }
      return
    }
    emit('login-success')
  } catch (e) {
    error.value = e.message
  } finally {
    loading.value = false
  }
}
</script>
