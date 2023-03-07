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
            endpointCop: "http://image.tmdb.org/t/p/w342/",
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
    <div class="col d-grid gap-3 my-2 box d-flex flex-column align-items-center flip-card">

        <div class="flip-card-inner">

            <div class="flip-card-front">
                <img :src="endpointCop + img" alt="">
            </div>

            <div class="flip-card-back">
                <h4 class="p-2 text-white">Titolo: {{ titolo }}</h4>
                <h4 class="p-2 text-white">Titolo originale: {{ titoloCer }}</h4>
                <div class="d-flex px-2">
                    <h4>Paese: </h4>
                    <img :src="getFlag(lingua)" class="ml-1">
                </div>
                <span class="d-flex align-items-center">
                    <h4>Critica: </h4>
                    <font-awesome-icon icon="fa-solid fa-star" class="text-white" v-for="i in star" />
                    <font-awesome-icon icon="fa-regular fa-star" class="text-white" v-for="i in (5 - star)" />
                </span>
            </div>

        </div>
    </div>
</template>

<style lang="scss" scoped>
.flip-card {
    background-color: transparent;
    perspective: 1000px;
    width: 300px;
    height: 400px;
}

.flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    transition: transform 0.6s;
    transform-style: preserve-3d;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

.flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
    cursor: pointer;
}

.flip-card-front,
.flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}

.flip-card-front img {
    width: 100%;
    height: 100%;
}

.flip-card-back {
    background-color: black;
    color: white;
    transform: rotateY(180deg);
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: start;
    padding: 15px;

}
</style>