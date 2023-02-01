<template>
    <nav class="navbar navbar-expand-lg bg-light">
        <div class="container-fluid">
            <RouterLink class="navbar-brand" to="/">Shopping Web</RouterLink>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup"
                aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
                <div class="navbar-nav ms-auto">
                    <RouterLink to="/about" class="nav-link">About US</RouterLink>
                    <RouterLink to="/about" class="nav-link">Product</RouterLink>
                    <RouterLink to="/about" class="nav-link">Shopping-cart</RouterLink>
                    <RouterLink to="/member" class="nav-link">Member Area</RouterLink>
                    <RouterLink to="/member" class="nav-link" @click.prevent="logOut()">Logout</RouterLink>
                </div>
            </div>
        </div>
    </nav>
</template>

<script setup>
import axios from 'axios';
import { useRouter } from 'vue-router'
const router = useRouter()


function logOut() {
    const api = `${import.meta.env.VITE_APP_PATH}logout`
    axios.post(api)
        .then((res) => {
            console.log(res)
            if (res.data.success) {
                router.push('/member')
            }
        })
        .catch((err) => {
            console.log(err)
        })
}

</script>