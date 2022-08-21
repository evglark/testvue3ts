<script lang="ts">
import Accordion from '@/components/Accordion/accordion.vue';
export default {
    components: { Accordion },
    data() {
        return {
            groupsOfProducts: [],
            timer: null,
        }
    },
    methods: {
        getData(): void {
            console.log(0);
            Promise.all([
                fetch('./src/data/data.json').then(response => response.json()),
                fetch('./src/data/names.json').then(response => response.json()),
            ]).then(([data, names]) => {
                const goods = data.Value.Goods;
                const uniqGroupsById = [...new Set(goods.map((el: any) => el.G))];
                const products = goods.map((el: any) => ({
                    groupId: el.G,
                    producrId: el.T,
                    name: names[el.G].B[el.T].N,
                    type: names[el.G].G,
                    quantity: el.P,
                    price: el.C,
                }));

                this.groupsOfProducts = uniqGroupsById.map(item =>
                    products.filter((el: any) => el.groupId === item)
                );
            });
        },
        clickHandler(props: any): void {
            console.log(JSON.parse(JSON.stringify(props)));
        },
        startTimer(func: () => any, timer: number): any {
            this.timer = setInterval(() => {
                func();
            }, timer);
        },
    },
    mounted() {
        this.getData();
        this.startTimer(this.getData, 15000_0);
    },
    beforeDestroy() {
        clearInterval(this.timer);
    }
}
</script>

<template>
    <main>
        <button v-on:click="getData">data</button>
        <Accordion
            v-for="(group) in this.groupsOfProducts"
            :title="group[0].type"
            :products="group"
            :onClick="this.clickHandler"
        />
    </main>
</template>