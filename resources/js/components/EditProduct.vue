<template>
    <div>
        <h3 class="text-center">Edit TTV</h3>
        <div class="row">
            <div class="col-md-6">
                <form @submit.prevent="updateProduct">
                    <div class="form-group">
                        <label>Name</label>
                        <input
                            type="text"
                            class="form-control"
                            v-model="product.name"
                        />
                    </div>
                    <div class="form-group">
                        <label>Tekanan Darah</label>
                        <input
                            type="text"
                            class="form-control"
                            v-model="product.tekanan"
                        />
                    </div>
                    <div class="form-group">
                        <label>Denyut Jantung</label>
                        <input
                            type="text"
                            class="form-control"
                            v-model="product.denyut"
                        />
                    </div>
                    <div class="form-group">
                        <label>Laju Pernapasan</label>
                        <input
                            type="text"
                            class="form-control"
                            v-model="product.laju"
                        />
                    </div>
                    <div class="form-group">
                        <label>Suhu</label>
                        <input
                            type="text"
                            class="form-control"
                            v-model="product.suhu"
                        />
                    </div>
                    <button type="submit" class="btn btn-primary">
                        Update
                    </button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            product: {},
        };
    },
    created() {
        this.axios
            .get(`http://localhost:8000/api/products/${this.$route.params.id}`)
            .then((res) => {
                this.product = res.data;
            });
    },
    methods: {
        updateProduct() {
            this.axios
                .patch(
                    `http://localhost:8000/api/products/${this.$route.params.id}`,
                    this.product
                )
                .then((res) => {
                    this.$router.push({ name: "home" });
                });
        },
    },
};
</script>
