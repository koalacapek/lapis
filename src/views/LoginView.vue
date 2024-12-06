<script setup lang="ts">
import { reactive } from 'vue'
import { RouterLink } from 'vue-router'
import { Form, Input, Button } from 'ant-design-vue'
import { UserOutlined, LockOutlined } from '@ant-design/icons-vue'

// Define the form state interface
interface FormState {
  email: string
  password: string
  remember: boolean
}

// Reactive form state
const formState = reactive<FormState>({
  email: '',
  password: '',
  remember: true,
})

// Form submission handler
const onFinish = (values: FormState) => {
  console.log('Form submitted with:', values)
}
</script>

<template>
  <div class="min-w-screen min-h-screen flex items-center justify-center">
    <div class="max-w-lg w-full shadow-xl rounded-xl p-5 text-center">
      <h1 class="text-2xl font-semibold text-center mb-4">Welcome!</h1>
      <Form
        :model="formState"
        class="text-left"
        :initial-values="{ remember: true }"
        @finish="onFinish"
      >
        <!-- Email Input -->
        <Form.Item
          name="email"
          :rules="[
            { required: true, message: 'Please input your email!' },
            { type: 'email', message: 'Please enter a valid email address!' },
          ]"
        >
          <Input v-model:value="formState.email" placeholder="Email" class="border-gray-400">
            <template #prefix>
              <UserOutlined />
            </template>
          </Input>
        </Form.Item>

        <!-- Password Input -->
        <Form.Item
          name="password"
          :rules="[{ required: true, message: 'Please input your Password!' }]"
        >
          <Input.Password
            v-model:value="formState.password"
            placeholder="Password"
            class="border-gray-400"
          >
            <template #prefix>
              <LockOutlined />
            </template>
          </Input.Password>
        </Form.Item>

        <!-- Submit Button -->
        <div class="text-center">
          <Form.Item>
            <Button type="primary" html-type="submit" class="w-full">Log in</Button>
            <div class="mt-3">
              <span class="text-gray-500 font-light">
                Don't have an account?
                <RouterLink to="/register" class="text-gray-800 font-medium"
                  >Register now!</RouterLink
                >
              </span>
            </div>
          </Form.Item>
        </div>
      </Form>
    </div>
  </div>
</template>

<style scoped>
/* Add any custom styles if needed */
</style>
