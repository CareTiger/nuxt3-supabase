import { UButton } from '../.nuxt/components';
import { _lineClamp } from '../.nuxt/tailwind.config';
<template>
    <UContainer class="h-screen w-full">
        <header>
            <nav class="h-16 flex flex-row space-x-6 justify-between items-center">
                <ColorModeSwitch />
                <div class="flex flex-row space-x-6">
                    <UButton v-if="!supabaseUser" icon="i-heroicons-question-mark-circle" size="sm" color="gray" variant="ghost" label="Forgot password" to="/forgot" :trailing="false"  />                
                    <UButton v-if="!supabaseUser"  icon="i-heroicons-pencil-square" size="sm" color="gray" variant="ghost" label="Sign up" to="/signup" :trailing="false"  />
                    <UButton v-if="!supabaseUser"  icon="i-heroicons-arrow-left-on-rectangle-20-solid" size="sm" color="primary" variant="solid" label="Sign in" to="/signin" :trailing="false"  />
                    <UButton v-if="supabaseUser"  icon="i-heroicons-arrow-right-on-rectangle-20-solid" size="sm" color="primary" variant="solid" label="Logout" to="/signin" :trailing="false" @click="logout"  />
                </div>
            </nav>
        </header>

        <div class="min-h-screen grid place-items-center">
            <slot />
        </div>

        <UNotifications />
    </UContainer>
</template>
<script setup lang="ts">
const supabaseUser = useSupabaseUser();
const supabaseAuthClient = useSupabaseAuthClient();
const toast = useToast();

const logout = async () => {
    await supabaseAuthClient.auth.signOut();
    toast.add({ title: 'Logged out', color: 'primary' });
}
</script>