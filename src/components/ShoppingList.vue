<template>
    <h3>Mi lista de compras</h3>
    <table class="table" v-if="itemsList.length > 0">
        <thead>
            <tr>
                <th scope="col">Nombre</th>
                <th scope="col">Valor unitario</th>
                <th scope="col">Cantidad</th>
                <th scope="col">Total</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in itemsList" :key="item.id">
                <th scope="row">{{item.name}}</th>
                <td>${{item.price}} COP</td>
                <td>{{item.quantity}}</td>
                <td>{{item.total}}</td>
            </tr>
        </tbody>
    </table>
    <EmptyList v-else/>
</template>

<script>
import EmptyList from './EmptyList.vue'

export default {
    name: 'ShoppingList',
    props: ['itemsList'],
    components: {
        EmptyList
    }
}
</script>