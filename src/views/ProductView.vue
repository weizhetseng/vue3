<template>
    <div class="text-end mt-3">
        <button class="btn btn-primary" type="button" @click="productModal.showModal()">
            新增商品
        </button>
    </div>
    <table class="table mt-4">
        <thead>
            <tr>
                <th width="120">分類</th>
                <th width="120">產品名稱</th>
                <th width="120">原價</th>
                <th width="120">售價</th>
                <th width="100">是否啟用</th>
                <th width="150">編輯</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="product in productList" :key="product.id">
                <td>{{ product.category }}</td>
                <td>{{ product.content }}</td>
                <td class="text-right">
                    {{ product.origin_price }}
                </td>
                <td class="text-right">
                    {{ product.price }}
                </td>
                <td>
                    <span class="text-success" v-if="product.is_enabled">啟用</span>
                    <span class="text-muted" v-else>未啟用</span>
                </td>
                <td>
                    <div class="btn-group">
                        <button class="btn btn-outline-primary btn-sm">編輯</button>
                        <button class="btn btn-outline-danger btn-sm">刪除</button>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
    <ProductModal ref="productModal"></ProductModal>

</template>

<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';
import ProductModal from '../components/productModal.vue';

const productList = ref([])
const productModal = ref(null)

onMounted(() => {
    const api = `${import.meta.env.VITE_APP_PATH}api/${import.meta.env.VITE_APP_API}/admin/products?page=:page`;
    axios.get(api)
        .then((res) => {
            console.log(res)
            productList.value = res.data.products
            console.log(productList)
        })
        .catch((err) => {
            console.log(err)
        })
})
</script>

<style lang="scss" scoped>
table {
    text-align: center;
}
</style>