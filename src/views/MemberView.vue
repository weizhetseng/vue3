<template>
    <div class="container mt-5">
        <form class="row justify-content-center" @submit.prevent="signIn">
            <div class="col-md-6">
                <h1 class="h3 mb-3 font-weight-normal">請先登入</h1>
                <div class="mb-2">
                    <label for="inputEmail" class="sr-only">Email address</label>
                    <input type="email" id="inputEmail" class="form-control" placeholder="Email address" required
                        autofocus autocomplete="off" v-model="user.username" />
                </div>
                <div class="mb-2">
                    <label for="inputPassword" class="sr-only">Password</label>
                    <input type="password" id="inputPassword" class="form-control" placeholder="Password" required
                        autocomplete="off" v-model="user.password" />
                </div>

                <div class="text-end mt-4">
                    <button class="btn btn-lg btn-primary btn-block" type="submit">登入</button>
                </div>
            </div>
        </form>
    </div>
</template>


<script setup>
import axios from 'axios'
import { useRouter } from 'vue-router';
const router = useRouter()

const user = {
    username: "springonionegg@gmail.com",
    password: "Thisisme851231",
}

function signIn() {
    const api = `${import.meta.env.VITE_APP_PATH}admin/signin`;
    axios.post(api, user)
        .then((res) => {
            console.log(res)
            if (res.data.success) {
                const token = res.data.token;
                const expired = res.data.expired;
                document.cookie = `weiToken=${token}`;
                document.cookie = `expires=${expired}`;
                router.push('/dashboard/product')
            }
        })
        .catch((err) => {
            console.log(err)
        })

}
</script>