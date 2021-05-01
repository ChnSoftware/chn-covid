<template>
    <div class="grid md:grid-cols-2 gap-4">
        <div class="shadow-md bg-purple-100 p-10 text-center rounded">
            <h3 class="text-3xl text-purple-900 font-bold mb-4">Vaka Sayısı</h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">Yeni:</span>
                {{ numberWithCommas(stats.NewConfirmed) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Toplam:</span>
                {{ numberWithCommas(stats.TotalConfirmed) }}
            </div>
        </div>

        <div class="shadow-md bg-purple-100 p-10 text-center rounded">
            <h3 class="text-3xl text-purple-900 font-bold mb-4">Ölüm Sayısı</h3>
            <div class="text-2xl mb-4">
                <span class="font-bold">Yeni:</span>
                {{ numberWithCommas(stats.NewDeaths) }}
            </div>
            <div class="text-2xl mb-4">
                <span class="font-bold">Toplam:</span>
                {{ numberWithCommas(stats.TotalDeaths) }}
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "DataBoxes",
        props: ["stats"],
        methods: {
            numberWithCommas(x) {
                return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
            }
        }
    }
</script>

<style>
</style>