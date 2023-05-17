<template>
    <div>
        <h2 class="text-center">Tanda Tanda Vital (TTV)</h2>

        <table class="table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nama</th>
                    <th>Tekanan Darah</th>
                    <th>Denyut Nadi</th>
                    <th>Laju Pernapasan</th>
                    <th>Suhu Tubuh</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="product in products" :key="product.id">
                    <td>{{ product.id }}</td>
                    <td>{{ product.name }}</td>
                    <td>{{ product.tekanan }}</td>
                    <td>{{ product.denyut }}</td>
                    <td>{{ product.laju }}</td>
                    <td>{{ product.suhu }}</td> 
                    <td>
                        <div class="btn-group" role="group">
                            <router-link
                                :to="{
                                    name: 'edit',
                                    params: { id: product.id },
                                }"
                                class="btn btn-success"
                                >Edit</router-link
                            >
                            <button
                                class="btn btn-danger"
                                @click="deleteProduct(product.id)"
                            >
                                Delete
                            </button>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    data() {
        return {
            products: [],
        };
    },
    created() {
        this.axios
            .get("http://localhost:8000/api/products/")
            .then((response) => {
                this.products = response.data;
            });
    },
    methods: {
        deleteProduct(id) {
            this.axios
                .delete(`http://localhost:8000/api/products/${id}`)
                .then((response) => {
                    let i = this.products.map((data) => data.id).indexOf(id);
                    this.products.splice(i, 1);
                });
        },
    },
};
</script>
