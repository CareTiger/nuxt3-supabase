<template>
    <div>
        <h1 class="text-4xl">Sign in</h1>
        <form class="flex flex-col space-y-6 mt-6 w-64" @submit.prevent="signin">
            <UFormGroup name="email" label="Email"><UInput type="email" placeholder="Email" v-model="email" /></UFormGroup>
            <UFormGroup name="password" label="Password"><UInput type="password" placeholder="Password" v-model="password"  /></UFormGroup>            
            <UButton block type="submit" label="Sign in" />
        </form>
    </div>
</template>
<script setup lang="ts">
const supabaseAuthClient = useSupabaseAuthClient();
const toast = useToast();

const email = ref('');
const password = ref('');
const signin = async () => {
    const { data, error } = await supabaseAuthClient.auth.signInWithPassword({ email: email.value, password: password.value });
    if (error) {
        toast.add({ title: "Oops! there was an error", description: error.message, color: 'red' });
    } else {
        toast.add({ title: 'Check your email for the confirmation link', color: 'primary' });
    }
}
</script>
```