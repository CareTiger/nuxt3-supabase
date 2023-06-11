<template>
    <div>
        <h1 class="text-4xl">Reset password</h1>
        <form class="flex flex-col space-y-6 mt-6 max-w-xs" @submit.prevent="forgot">
            <UFormGroup name="password" label="Password"><UInput type="password" placeholder="Password" v-model="password" /></UFormGroup>       
            <UFormGroup name="repeat_password" label="Repeat Password"><UInput type="password" placeholder="Repeat Password" v-model="repeat_password" /></UFormGroup>       
            <UButton block type="submit" label="Send reset link" />
        </form>
    </div>
</template>
<script setup lang="ts">
const supabaseAuthClient = useSupabaseAuthClient();
const toast = useToast();

const password = ref('');
const repeat_password = ref('');

const forgot = async () => {
    const { error } = await supabaseAuthClient.auth.resetPasswordForEmail(password.value);
    if (error) {
        toast.add({ title: "Oops! there was an error", description: error.message, color: 'red' });
    } else {
        toast.add({ title: 'Done!', color: 'primary' });
    }
}
</script>