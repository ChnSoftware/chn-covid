<template>
    <main v-if="!loading">
        <DataTitle :dataDate="dataDate" :text="title" />
        <DataBoxes :stats="stats" />
        <CountrySelect @get-country="getCountryData" :countries="countries" />
        <button
            @click="clearCountryData"
            v-if="stats.Country"
            class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
        >
            Temizle
        </button>
    </main>
    <main v-else class="flex flex-col align-center justify-center text-center">
        <div class="text-gray-500 text-3xl mt-10 mb-6">Veriler Alınıyor...</div>
        <img :src="loadingImage" class="w-24 m-auto" alt="" />
    </main>
</template>

<script>
    import DataTitle from "@/components/DataTitle"
    import DataBoxes from "@/components/DataBoxes"
    import CountrySelect from "@/components/CountrySelect"

    export default {
        name: 'Home',
        components: {
            DataTitle,
            DataBoxes,
            CountrySelect
        },
        data() {
            return {
                loading: true,
                title: "Dünya Çapında Vaka ve Ölüm Sayıları",
                dataDate: "",
                stats: {},
                countries: [],
                // loadingImage: require("@/assets/hourglass.gif"),
                loadingImage: require("../assets/hourglass.gif"),
            }
        },
        methods: {
            async fetchCovidData() {
                const res = await fetch("https://api.covid19api.com/summary")
                const data = await res.json()
                return data
            },
            getCountryData(country) {
                this.stats = country
                this.title = country.Country
            },
            async clearCountryData() {
                this.loading = true
                const data = await this.fetchCovidData()
                this.stats = data.Global
                this.title = "Dünya Çapında Vaka ve Ölüm Sayıları"
                this.loading = false
            }
        },
        async created() {
            const data = await this.fetchCovidData()

            this.dataDate = data.Date
            this.stats = data.Global
            this.countries = data.Countries
            this.loading = false
        }
    }
</script>
