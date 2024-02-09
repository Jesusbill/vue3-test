<template>
    <div>
        <h1>User ID from Cookie</h1>
        <p v-if="userId">User ID: {{ userId }}</p>
        <p v-else>Loading...</p>
    </div>
</template>
  
<script>
import { onMounted } from 'vue';
import { useUserStore } from '@/stores/user.js'; // Import your Pinia store
import { storeToRefs } from 'pinia'


export default {
    setup() {
        
        const { userId } = storeToRefs(useUserStore())

        // Read the user ID from the cookie during component mounting
        onMounted(() => {
            console.log(document.cookie)
            const cookieValue = document.cookie
                .split('; ')
                .find((row) => row.startsWith('picalc_exchangeuserid='))
                ?.split('=')[1];

            console.log(document.cookieValue)
            // Set the userId ref with the value from the cookie
            userId.value = cookieValue || null;
        });

        return {
            userId,
        };
    },
};
</script>
  
<style>
/* Add your component styles here */
</style>
  