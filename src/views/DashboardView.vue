<template>
    <div class="container">
        <RouterView></RouterView>
    </div>
</template>


<script setup>
import axios from 'axios';
import { onMounted } from 'vue';
import { useRouter } from 'vue-router'
const router = useRouter()


onMounted(() => {
    const token = document.cookie.replace(/(?:(?:^|.*;\s*)weiToken\s*=\s*([^;]*).*$)|^.*$/, '$1');
    axios.defaults.headers.common['Authorization'] = `${token}`
    const api = `${import.meta.env.VITE_APP_PATH}api/user/check`
    axios.post(api)
        .then((res) => {
            if (!res.data.success) {
                router.push('/member')
            }
        })
        .catch((err) => {
            console.log(err)
        })
})
</script>