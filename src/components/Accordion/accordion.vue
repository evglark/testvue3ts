<script lang="ts">
export default {
    name: 'Accordion',
    props: {
        title: String,
        products: Array,
        onClick: Function,
    }
}
</script>

<template>
    <div class="accordion">
        <div class="header">{{ title }}</div>
        <div class="body">
            <div v-for="(product) in products" class="product-card" @click="onClick(product)">
                {{ product.selectd ? 1 : 0 }}
                <div class="name">{{ product.name }} ({{ product.quantity }})</div>
                <div class="price">{{ product.price }}</div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.accordion {
    color: black;
    margin: 8px 0 8px 0;
    border: 1px solid;
}

.header {
    padding: 4px;
    background-color: antiquewhite;
    border-radius: 8px 8px 0 0;
    border-bottom: 1px solid;
}

.body {
    display: flex;
    flex-wrap: wrap;
    background-color: aliceblue;
}

.product-card {
    display: flex;
    flex-basis: calc(50%);
    border-bottom: 1px solid;
    border-right: 1px solid;
}

.product-card:hover {
    cursor: pointer;
}

.name {
    width: 100%;
    padding: 4px;
}

.price {
    width: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: gray;
}
</style>