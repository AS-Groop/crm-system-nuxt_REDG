<script lang="ts" setup>
import {v4 as uuid} from 'uuid'
import {useIsLoadingStore, useAuthStore} from "~/stores/auth.store";

useSeoMeta({
  title: "Login | CRM system"
})

const email = ref('')
const password = ref('')
const name = ref('')

watch(email,()=>{
  console.log(email.value )
})

const isLoadingStore = useIsLoadingStore();
const authStore = useAuthStore()
const router = useRouter()

const login = async ()=> {
  isLoadingStore.set(true)
  await account.createEmailPasswordSession(email.value, password.value);
  const res = await account.get();
  if(res) {
    authStore.set({
      email: res.email,
      name: res.name,
      status: res.status
    })
  }
  email.value = '';
  password.value = '';
  name.value = '';
  await router.push('/')
  isLoadingStore.set(false)
}

const register = async ()=>{
  await account.create(uuid(), email.value, password.value, name.value)
  await login()
}

</script>

<template>
  <div class="flex items-center justify-center min-h-screen w-full">
    <div class="rounded bg-sidebar w-1/4 p-5">
      <h1 class="text-2xl font-bold text-center mb-5">Login</h1>
      <form>
        <UiInput v-model="email" placeholder="Email" type="email" class="mb-3"/>
        <UiInput v-model="password" placeholder="Password" type="password" class="mb-3"/>
        <UiInput v-model="name" placeholder="Name" type="text" class="mb-3"/>
        <div class="flex items-center justify-center gap-5">
          <UiButton @click="login" type="button">Login</UiButton>
          <UiButton @click="register" type="button">Register</UiButton>
        </div>
      </form>
    </div>
  </div>
</template>
