<template>
    <main class="container mt-5">
        <div class="row">
            <div class="col-12 text-right mb-4">
                <div class="d-flex justify-content-between">
                    <h3>育てた水草一覧</h3>
                    <nuxt-link to="/waterplants/add" class="btn btn-info">
                        水草を追加する
                    </nuxt-link>
                </div>
            </div>
            <template v-for="waterplant in waterplants">
                <div :key="waterplant.id" class="col-lg-3 col-md-4 col-sm-6 mb-4">
                    <water-plant-card 
                    :onDelete="deleteWaterPlant" 
                    :waterplant="waterplant">
                    </water-plant-card>
                </div>
            </template>
        </div>
    </main>
</template>
<script>
import WaterPlantCard from '~/components/WaterPlantCard.vue';

const sampleDate = [
    {
        id: 1,
        name: 'サンプルパールグラス',
        position: '中景〜後景',
        picture: '/images/banner.jpg',
        difficulty: 'Easy',
        addition_amount: 'High',
        leaf_length: 2,
        water_quality: '弱酸性〜中性　軟水〜弱硬水'
    },
    {
        d: 2,
        name: 'サンプルキューバパールグラス',
        position: '前景',
        picture: '/images/banner.jpg',
        difficulty: 'Hard',
        addition_amount: 'High',
        leaf_length: 1,
        water_quality: '弱酸性〜中性　軟水〜弱硬水'
    },
    {
        d: 3,
        name: 'サンプルニューラージパールグラス',
        position: '前景',
        picture: '/images/banner.jpg',
        difficulty: 'Medium',
        addition_amount: 'High',
        leaf_length: 1,
        water_quality: '弱酸性〜中性　軟水〜弱硬水'
    }
]

export default {
    head () {
        return {
            title: '水草一覧'
        }
    },
    conponents: {
        WaterPlantCard
    },
    data () {
        return {
            waterplants: [],
            url: "http://localhost:8000/api/waterplants/"
        }
    },
    async asyncData ( { $axios, params } ) {
        try{
            const waterplants = await $axios.$get(`/waterplants/`)
            return { waterplants: waterplants }
        }catch(e){
            return { waterplants: [] }
        }
    },
    methods: {
        async deleteWaterPlant ( waterplant_id ) {
            try {
                await this.$axios.$delete(`/waterplants/${waterplant_id}/`)
                const newWaterPlants = await this.$axios.$get(`/waterplants/`)
                this.waterplants = newWaterPlants
            } catch (e) {
                console.log(e)
            }
        }
    }
}
</script>
<style scoped>
</style>