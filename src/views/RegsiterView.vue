<script setup lang="ts">
import { reactive, ref } from 'vue'
import { Form, Input, Button, message } from 'ant-design-vue'
import { useRouter, RouterLink } from 'vue-router'

// Form state and validation rules
const formState = reactive({
  fullname: '',
  email: '',
  dob: '',
  hospitalName: '',
  specialization: '',
  location: '',
  phone: '',
  password: '',
  confirm: '',
})

const passwordPattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/

const error = ref('')
const router = useRouter()

const onFinish = () => {
  if (!formState.password) {
    message.error('Password is required!')
    return
  }
  if (formState.password !== formState.confirm) {
    message.error('Passwords do not match!')
    return
  }
  message.success('Form submitted successfully!')
  console.log('Form State:', formState)
}
</script>

<template>
  <div class="min-w-screen min-h-screen flex items-center justify-center">
    <div class="max-w-xl w-full p-7 shadow-xl rounded-lg">
      <h1 class="text-2xl font-semibold text-center mb-4">Register</h1>

      <Form
        layout="vertical"
        :model="formState"
        name="register"
        @finish="onFinish"
        class="text-left"
        :scroll-to-first-error="true"
      >
        <!-- Full Name -->
        <Form.Item
          name="fullname"
          label="Full Name"
          class="mb-4"
          :rules="[{ required: true, message: 'Please input your full name!', whitespace: true }]"
        >
          <Input p laceholder="Full Name" v-model:value="formState.fullname" class="w-full" />
        </Form.Item>

        <!-- Email -->
        <Form.Item
          name="email"
          label="E-mail"
          class="mb-2"
          :rules="[
            { type: 'email', message: 'Please input a valid email!' },
            { required: true, message: 'Please input your E-mail!' },
          ]"
        >
          <Input placeholder="example@email.com" v-model:value="formState.email" />
        </Form.Item>

        <!-- Password -->
        <Form.Item
          name="password"
          label="Password"
          class="mb-2"
          :rules="[
            { required: true, message: 'Please input your password!' },
            { pattern: passwordPattern, message: 'Password must meet the requirements!' },
          ]"
          has-feedback
        >
          <Input.Password v-model:value="formState.password" />
        </Form.Item>

        <!-- Confirm Password -->
        <Form.Item
          name="confirm"
          label="Confirm Password"
          class="mb-2"
          :rules="[{ required: true, message: 'Please confirm your password!' }]"
          has-feedback
        >
          <Input.Password v-model:value="formState.confirm" />
        </Form.Item>

        <!-- Submit Button -->
        <Form.Item>
          <a-button type="primary" html-type="submit" class="w-full mt-4">Register</a-button>
          <p v-if="error" class="text-red-500 text-center mt-2">{{ error }}</p>
          <div class="mt-3 text-center">
            <span class="text-gray-500 font-light">
              Already have an account?
              <RouterLink to="/login" class="text-gray-800 font-medium">Login now!</RouterLink>
            </span>
          </div>
        </Form.Item>
      </Form>
    </div>
  </div>
</template>
