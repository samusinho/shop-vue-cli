<template>
    <h3>Le ofrecemos</h3>
    <div class="row">
        <div class="col-4" v-for="product in products" :key="product.id">
            <div class="card">
                <img :src="product.image" alt=""
                class="card-img-top" height="250">
                <div class="card-body">
                    <h5 class="card-title">
                        {{product.name}}
                    </h5>
                    <p>En stock: <b>{{product.stock}}</b></p>
                    <p class="card-text">
                        Delicioso/a {{product.name.toLowerCase()}} a tan solo <b>${{product.price}}</b> pesitos el kilo.
                    </p>
                    <button class="btn btn-primary me-1"
                    v-on:click="additem(product.name)"
                    :disabled="product.stock == 0">Añadir 1</button>
                    <button class="btn btn-danger"
                    v-on:click="removeitem(product.name)"
                    :disabled="disableButton(product.name)">Quitar 1</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Products',
    props: [
        'products',
        'disableButton'
    ],
    methods: {
        additem(name) {
            this.$emit('addItem', name);
        },
        removeitem(name) {
            this.$emit('removeItem', name);
        },
    }
}
</script>