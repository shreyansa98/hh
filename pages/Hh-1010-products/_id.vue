<template>
<body>
    <main>
        <div class="container">
            <div class="row">
                    <div class="col-12">
                        <div class="a-spacing-top-medium"></div>
                        <h2 class="mt-2" style="text-align: center">Update {{product.title}}</h2>
                        <form>
                            <!-- Category Dropdown -->
                            <div class="a-spacing-top-medium">
                                <label>Category</label>
                                <select class="a-select-option" v-model="categoryID">
                                    <option v-for="category in categories" :value="category._id" :key="category._id">{{category.type}}</option>
                                </select>
                            </div>

                            <!-- Owner Dropdown -->
                            <div class="a-spacing-top-medium">
                                <label>Owner</label>
                                <select class="a-select-option" v-model="ownerID">
                                    <option v-for="owner in owners" :value="owner._id" :key="owner._id">{{owner.name}}</option>
                                </select>
                            </div>

                            <!-- Title -->
                            <div class="a-spacing-top-medium">
                                <label style="margin-bottom: 0px">Title</label>
                                <input type="text" class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info" style="width: 100%" v-model="title" :placeholder="product.title"/>
                            </div>

                             <!-- Price -->
                            <div class="a-spacing-top-medium">
                                <label style="margin-bottom: 0px">Price</label>
                                <input type="number" class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info" style="width: 100%" v-model="price" :placeholder="product.price"/>
                            </div>

                            <!-- stockQuantity -->
                            <div class="a-spacing-top-medium">
                                <label style="margin-bottom: 0px">Stock Quantity</label>
                                <input type="number" class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info" style="width: 100%" v-model="stockQuantity" :placeholder="product.stockQuantity"/>
                            </div>

                             <!-- Description -->
                            <div class="a-spacing-top-medium">
                                <label style="margin-bottom: 0px">Description</label>
                                <textarea class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info" style="width: 100%" v-model="description" :placeholder="product.description"></textarea>
                            </div>

                            <!-- Photo -->
                            <div class="a-spacing-top-medium">
                                <label style="margin-bottom: 0px">Add Photo</label>
                                <div class="a-row a-spacing-top-medium">
                                    <label class="choosefile-button">
                                        <input type="file" @change="onFileSelected" />
                                        <p style="margin-top: -70px">
                                           {{ fileName}}
                                        </p>
                                    </label>
                                </div>
                            </div>
                            <hr>
                            <!-- Button -->
                            <div class="a-spacing-top-large">
                                <span class="a-button-register">
                                    <span class="a-button-inner">
                                        <span class="btn btn-small btn-dark" @click="onUpdateProduct">
                                            Update Product
                                        </span>
                                    </span>
                                </span>
                            </div>
                        </form>
                    </div>
            </div>
        </div>
    </main>
    </body>
</template>

<script>
export default {
    async asyncData({ $axios, params}){
        try{
            let categories = $axios.$get("/api/categories");
            let owners = $axios.$get("/api/owners");
            let product = $axios.$get(`/api/products/${params.id}`);

            const [catResponse, ownerResponse, productResponse] = await Promise.all([
                categories,
                owners,
                product
            ]);

            return {
                categories: catResponse.categories,
                owners: ownerResponse.owners,
                product: productResponse.product
            }
        } catch (err){
            console.log(err);
        }
    },

    data() {
        return {
            categoryID: null,
            ownerID: null,
            title: "",
            price: "",
            description: "",
            stockQuantity: "",
            selectedFile: null,
            fileName: ""
        }
    },

    methods: {
        onFileSelected(event) {
            this.selectedFile = event.target.files[0];
            console.log(this.selectedFile); 
            this.fileName = event.target.files[0].name;
        },

        async onUpdateProduct() {
            let data = new FormData();
            data.append("title", this.title);
            data.append("price", this.price);
            data.append("stockQuantity", this.stockQuantity);
            data.append("description", this.description);
            data.append("ownerID", this.ownerID);
            data.append("categoryID", this.categoryID);
            data.append("photo", this.selectedFile, this.selectedFile.name);

            let result = await this.$axios.$put(`/api/products/${this.$route.params.id}`, data);

            this.$router.push("/Hh-1010-index");
        }
    }
    
}
</script>