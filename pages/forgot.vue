<template>
    <div>
        <h1 class="text-4xl">Forgot</h1>
        <form class="flex flex-col space-y-6 mt-6 w-64" @submit.prevent="forgot">
            <UFormGroup name="email" label="Email"><UInput type="email" placeholder="Email" v-model="email" /></UFormGroup>       
            <UButton block type="submit" label="Send reset link" />
        </form>
    </div>
</template>
<script setup lang="ts">
const supabaseAuthClient = useSupabaseAuthClient();
const toast = useToast();

const email = ref('');

const forgot = async () => {
    const { data, error } = await supabaseAuthClient.auth.resetPasswordForEmail(email.value, { redirectTo: 'http://localhost:3000/reset' });
    if (error) {
        toast.add({ title: "Oops! there was an error", description: error.message, color: 'red' });
    } else {
        toast.add({ title: 'Check your email for the reset link', color: 'primary' });
    }
}
</script>