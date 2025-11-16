<template>
  <div class="login-container">
    <div class="login-card">
      <!-- 头部 -->
      <div class="login-header">
        <div class="logo-section">
          <div class="logo-icon">
            <svg width="48" height="48" viewBox="0 0 48 48" fill="none">
              <circle cx="24" cy="24" r="20" fill="#42b883" opacity="0.1"/>
              <path d="M24 8C15.16 8 8 15.16 8 24s7.16 16 16 16 16-7.16 16-16S32.84 8 24 8zm0 4c3.32 0 6 2.68 6 6s-2.68 6-6 6-6-2.68-6-6 2.68-6 6-6zm0 28c-4.84 0-9.14-2.44-11.68-6.16.08-3.8 7.6-5.88 11.68-5.88s11.6 2.08 11.68 5.88C33.14 37.56 28.84 40 24 40z" fill="#42b883"/>
            </svg>
          </div>
          <h1 class="app-title">欢迎回来</h1>
          <p class="app-subtitle">请登录您的账户以继续</p>
        </div>
      </div>

      <!-- 登录表单 -->
      <form @submit.prevent="handleLogin" class="login-form">
        <!-- 用户名输入 -->
        <div class="form-group">
          <label for="username" class="form-label">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
              <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 3c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm0 14.2c-2.5 0-4.71-1.28-6-3.22.03-1.99 4-3.08 6-3.08 1.99 0 5.97 1.09 6 3.08-1.29 1.94-3.5 3.22-6 3.22z" fill="#64748b"/>
            </svg>
            用户名
          </label>
          <input
            id="username"
            v-model="loginForm.username"
            type="text"
            class="form-input"
            :class="{ 'error': errors.username }"
            placeholder="请输入用户名"
            autocomplete="username"
            @blur="validateField('username')"
          />
          <span v-if="errors.username" class="error-message">{{ errors.username }}</span>
        </div>

        <!-- 密码输入 -->
        <div class="form-group">
          <label for="password" class="form-label">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
              <path d="M6 10v-4c0-3.31 2.69-6 6-6s6 2.69 6 6v4h2c1.1 0 2 .9 2 2v8c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2v-8c0-1.1.9-2 2-2h2zm6-8c-2.21 0-4 1.79-4 4v4h8v-4c0-2.21-1.79-4-4-4z" fill="#64748b"/>
            </svg>
            密码
          </label>
          <div class="password-input-wrapper">
            <input
              id="password"
              v-model="loginForm.password"
              :type="showPassword ? 'text' : 'password'"
              class="form-input"
              :class="{ 'error': errors.password }"
              placeholder="请输入密码"
              autocomplete="current-password"
              @blur="validateField('password')"
            />
            <button
              type="button"
              class="password-toggle"
              @click="showPassword = !showPassword"
            >
              <svg v-if="showPassword" width="20" height="20" viewBox="0 0 24 24" fill="none">
                <path d="M12 4.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5zM12 17c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5zm0-8c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3z" fill="#64748b"/>
              </svg>
              <svg v-else width="20" height="20" viewBox="0 0 24 24" fill="none">
                <path d="M12 7c2.76 0 5 2.24 5 5 0 .65-.13 1.26-.36 1.83l2.92 2.92c1.51-1.26 2.7-2.89 3.43-4.75-1.73-4.39-6-7.5-11-7.5-1.4 0-2.74.25-3.98.7l2.16 2.16C10.74 7.13 11.35 7 12 7zM2 4.27l2.28 2.28.46.46C3.08 8.3 1.78 10.02 1 12c1.73 4.39 6 7.5 11 7.5 1.55 0 3.03-.3 4.38-.84l.42.42L19.73 22 21 20.73 3.27 3 2 4.27zM7.53 9.8l1.55 1.55c-.05.21-.08.43-.08.65 0 1.66 1.34 3 3 3 .22 0 .44-.03.65-.08l1.55 1.55c-.67.33-1.41.53-2.2.53-2.76 0-5-2.24-5-5 0-.79.2-1.53.53-2.2zm4.31-.78l3.15 3.15.02-.16c0-1.66-1.34-3-3-3l-.17.01z" fill="#64748b"/>
              </svg>
            </button>
          </div>
          <span v-if="errors.password" class="error-message">{{ errors.password }}</span>
        </div>

        <!-- 记住我和忘记密码 -->
        <div class="form-options">
          <label class="checkbox-container">
            <input
              v-model="loginForm.remember"
              type="checkbox"
              class="checkbox"
            />
            <span class="checkmark"></span>
            记住我
          </label>
          <a href="#" class="forgot-password" @click.prevent="handleForgotPassword">忘记密码？</a>
        </div>

        <!-- 登录按钮 -->
        <button
          type="submit"
          class="login-button"
          :disabled="isLoading"
        >
          <span v-if="!isLoading">登录</span>
          <div v-else class="loading-spinner">
            <div class="spinner"></div>
            <span>登录中...</span>
          </div>
        </button>

        <!-- 错误提示 -->
        <div v-if="loginError" class="error-alert">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
            <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-2h2v2zm0-4h-2V7h2v6z" fill="#ef4444"/>
          </svg>
          {{ loginError }}
        </div>
      </form>

      <!-- 注册链接 -->
      <div class="register-section">
        <p class="register-text">
          还没有账户？
          <a href="#" class="register-link" @click.prevent="handleRegister">立即注册</a>
        </p>
      </div>

      <!-- 社交登录 -->
      <div class="social-login">
        <div class="divider">
          <span>或</span>
        </div>
        <div class="social-buttons">
          <button type="button" class="social-btn github" @click="handleSocialLogin('github')">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
            </svg>
            GitHub
          </button>
          <button type="button" class="social-btn google" @click="handleSocialLogin('google')">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
              <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
              <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
              <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
            </svg>
            Google
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, reactive, onMounted } from 'vue'

// 表单数据接口
interface LoginForm {
  username: string
  password: string
  remember: boolean
}

// 表单验证错误接口
interface FormErrors {
  username?: string
  password?: string
}

// 响应式表单数据
const loginForm = reactive<LoginForm>({
  username: '',
  password: '',
  remember: false
})

// 表单验证错误
const errors = reactive<FormErrors>({})

// UI状态
const showPassword = ref(false)
const isLoading = ref(false)
const loginError = ref('')

// 验证规则类型定义
interface BaseValidationRule {
  required?: boolean
  message: string
}

interface RequiredRule extends BaseValidationRule {
  required: true
}

interface MinLengthRule extends BaseValidationRule {
  minLength: number
}

interface PatternRule extends BaseValidationRule {
  pattern: RegExp
}

type ValidationRule = RequiredRule | MinLengthRule | PatternRule

// 验证规则对象类型
type ValidationRules = {
  [K in keyof LoginForm]?: ValidationRule[]
}

// 表单验证规则
const validationRules: ValidationRules = {
  username: [
    { required: true, message: '请输入用户名' },
    { minLength: 3, message: '用户名至少3个字符' },
    { pattern: /^[a-zA-Z0-9_]+$/, message: '用户名只能包含字母、数字和下划线' }
  ],
  password: [
    { required: true, message: '请输入密码' },
    { minLength: 6, message: '密码至少6个字符' }
  ]
}

// 验证单个字段
const validateField = (field: keyof FormErrors): boolean => {
  const value = loginForm[field as keyof LoginForm]
  const rules = validationRules[field]

  if (!rules) return true

  // 清除之前的错误
  delete errors[field]

  for (const rule of rules) {
    // 必填验证
    if ('required' in rule && rule.required && !value) {
      errors[field] = rule.message
      return false
    }

    // 最小长度验证（只对字符串类型有效）
    if ('minLength' in rule && typeof value === 'string' && value.length < rule.minLength) {
      errors[field] = rule.message
      return false
    }

    // 正则表达式验证（只对字符串类型有效）
    if ('pattern' in rule && typeof value === 'string' && !rule.pattern.test(value)) {
      errors[field] = rule.message
      return false
    }
  }

  return true
}

// 验证整个表单
const validateForm = (): boolean => {
  const usernameValid = validateField('username')
  const passwordValid = validateField('password')
  return usernameValid && passwordValid
}

// 处理登录
const handleLogin = async () => {
  loginError.value = ''

  if (!validateForm()) {
    return
  }

  isLoading.value = true

  try {
    // 模拟登录请求
    await new Promise(resolve => setTimeout(resolve, 1500))

    // 模拟登录验证
    if (loginForm.username === 'admin' && loginForm.password === '123456') {
      console.log('登录成功', { ...loginForm })
      // 这里可以跳转到其他页面或触发登录成功事件

      // 如果记住我，保存到localStorage
      if (loginForm.remember) {
        localStorage.setItem('rememberedUser', loginForm.username)
      }

      // 清除表单
      loginForm.password = ''
      loginForm.username = ''
      loginForm.remember = false

      alert('登录成功！')
    } else {
      loginError.value = '用户名或密码错误'
    }
  } catch (error) {
    console.error('登录错误:', error)
    loginError.value = '网络错误，请稍后重试'
  } finally {
    isLoading.value = false
  }
}

// 处理忘记密码
const handleForgotPassword = () => {
  console.log('处理忘记密码')
  alert('忘记密码功能暂未实现')
}

// 处理注册
const handleRegister = () => {
  console.log('处理注册')
  alert('注册功能暂未实现')
}

// 处理社交登录
const handleSocialLogin = (provider: string) => {
  console.log(`使用 ${provider} 登录`)
  alert(`${provider} 登录功能暂未实现`)
}

// 组件挂载时的初始化
onMounted(() => {
  // 检查是否有记住的用户名
  const rememberedUser = localStorage.getItem('rememberedUser')
  if (rememberedUser) {
    loginForm.username = rememberedUser
    loginForm.remember = true
  }

  // 为演示方便，添加提示信息
  console.log('测试账户: admin / 123456')
})
</script>

<style scoped>
.login-container {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 20px;
}

.login-card {
  background: white;
  border-radius: 16px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  width: 100%;
  max-width: 420px;
  padding: 40px 32px;
  animation: slideInUp 0.6s ease-out;
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.login-header {
  text-align: center;
  margin-bottom: 32px;
}

.logo-section {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.logo-icon {
  margin-bottom: 16px;
}

.app-title {
  font-size: 28px;
  font-weight: 700;
  color: #1f2937;
  margin: 0 0 8px 0;
}

.app-subtitle {
  font-size: 16px;
  color: #6b7280;
  margin: 0;
}

.login-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-label {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 500;
  color: #374151;
  margin-bottom: 8px;
}

.form-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #e5e7eb;
  border-radius: 8px;
  font-size: 14px;
  transition: all 0.2s;
  background: #f9fafb;
}

.form-input:focus {
  outline: none;
  border-color: #42b883;
  background: white;
  box-shadow: 0 0 0 3px rgba(66, 184, 131, 0.1);
}

.form-input.error {
  border-color: #ef4444;
}

.form-input.error:focus {
  box-shadow: 0 0 0 3px rgba(239, 68, 68, 0.1);
}

.password-input-wrapper {
  position: relative;
}

.password-toggle {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.2s;
}

.password-toggle:hover {
  background: #f3f4f6;
}

.error-message {
  color: #ef4444;
  font-size: 12px;
  margin-top: 4px;
}

.form-options {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
}

.checkbox-container {
  display: flex;
  align-items: center;
  cursor: pointer;
  user-select: none;
}

.checkbox {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: relative;
  display: inline-block;
  height: 18px;
  width: 18px;
  background-color: #f3f4f6;
  border: 2px solid #d1d5db;
  border-radius: 4px;
  margin-right: 8px;
  transition: all 0.2s;
}

.checkbox:checked ~ .checkmark {
  background-color: #42b883;
  border-color: #42b883;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
  left: 5px;
  top: 2px;
  width: 4px;
  height: 8px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

.checkbox:checked ~ .checkmark:after {
  display: block;
}

.forgot-password {
  color: #42b883;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.2s;
}

.forgot-password:hover {
  color: #35a87c;
}

.login-button {
  width: 100%;
  padding: 14px 20px;
  background: linear-gradient(135deg, #42b883 0%, #35a87c 100%);
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  position: relative;
  overflow: hidden;
}

.login-button:hover:not(:disabled) {
  transform: translateY(-1px);
  box-shadow: 0 8px 16px rgba(66, 184, 131, 0.3);
}

.login-button:active:not(:disabled) {
  transform: translateY(0);
}

.login-button:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

.loading-spinner {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.spinner {
  width: 16px;
  height: 16px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-top: 2px solid white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.error-alert {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 12px 16px;
  background: #fef2f2;
  border: 1px solid #fecaca;
  border-radius: 8px;
  color: #ef4444;
  font-size: 14px;
}

.register-section {
  text-align: center;
  margin-top: 24px;
  padding-top: 24px;
  border-top: 1px solid #e5e7eb;
}

.register-text {
  color: #6b7280;
  font-size: 14px;
  margin: 0;
}

.register-link {
  color: #42b883;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.2s;
}

.register-link:hover {
  color: #35a87c;
}

.social-login {
  margin-top: 24px;
}

.divider {
  text-align: center;
  position: relative;
  margin-bottom: 16px;
}

.divider::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  height: 1px;
  background: #e5e7eb;
}

.divider span {
  background: white;
  padding: 0 16px;
  color: #6b7280;
  font-size: 14px;
  position: relative;
}

.social-buttons {
  display: flex;
  gap: 12px;
}

.social-btn {
  flex: 1;
  padding: 10px 16px;
  border: 2px solid #e5e7eb;
  background: white;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 500;
  color: #374151;
  cursor: pointer;
  transition: all 0.2s;
}

.social-btn:hover {
  background: #f9fafb;
  border-color: #d1d5db;
}

.social-btn.github:hover {
  background: #24292e;
  border-color: #24292e;
  color: white;
}

.social-btn.google:hover {
  background: #f8f9fa;
  border-color: #d1d5db;
}

/* 响应式设计 */
@media (max-width: 480px) {
  .login-container {
    padding: 16px;
  }

  .login-card {
    padding: 32px 24px;
  }

  .app-title {
    font-size: 24px;
  }

  .social-buttons {
    flex-direction: column;
  }
}

/* 暗色模式支持 */
@media (prefers-color-scheme: dark) {
  .login-card {
    background: #1f2937;
    color: #f9fafb;
  }

  .app-title {
    color: #f9fafb;
  }

  .app-subtitle {
    color: #d1d5db;
  }

  .form-label {
    color: #e5e7eb;
  }

  .form-input {
    background: #374151;
    border-color: #4b5563;
    color: #f9fafb;
  }

  .form-input:focus {
    background: #4b5563;
  }

  .register-text {
    color: #d1d5db;
  }

  .social-btn {
    background: #374151;
    border-color: #4b5563;
    color: #e5e7eb;
  }

  .social-btn:hover {
    background: #4b5563;
  }

  .divider::before {
    background: #4b5563;
  }

  .divider span {
    background: #1f2937;
    color: #d1d5db;
  }
}
</style>
