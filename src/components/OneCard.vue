<script>

export default {
    props: {
        titolo: String,
        titoloCer: String,
        lingua: String,
        valutazione: Number,
        img: String,
    },

    data() {
        return {
            endpointFlag1: "https://flagcdn.com/20x15/",
            endpointFlag2: ".png",
            endpointCop: "http://image.tmdb.org/t/p/w185/",
            star: Math.floor(this.valutazione / 2),
        }
    },

    methods: {
        getFlag(nazione) {
            if (nazione == "en") return "https://flagcdn.com/24x18/us.png";
            if (nazione == "ja") return "https://flagcdn.com/24x18/jp.png";
            if (nazione == "ko") return "https://flagcdn.com/24x18/kr.png";
            if (nazione == "hi") return "https://flagcdn.com/24x18/in.png";



            return "https://flagcdn.com/24x18/" + nazione + ".png";
        },
    },

};
</script>

<template>
    <div class="col d-grid gap-3 my-2">

        <div class="box d-flex flex-column align-items-center">
            <img :src="endpointCop + img" alt="">
            <h3 class="p-2 text-white text-center">{{ titolo }}</h3>
            <h3 class="p-2 text-white text-center">{{ titoloCer }}</h3>
            <img :src="getFlag(lingua)">
            <!-- <h3 class="p-2 text-white text-center">{{ star }}</h3> -->
            <span class="">
                <font-awesome-icon icon="fa-solid fa-star" class="text-white" v-for="i in star" />
                <font-awesome-icon icon="fa-regular fa-star" class="text-white" v-for="i in (5 - star)" />
            </span>

        </div>
    </div>
</template>

<style lang="scss" scoped></style>