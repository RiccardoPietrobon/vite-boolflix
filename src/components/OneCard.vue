<script>


export default {
    props: {
        titolo: String,
        titoloCer: String,
        lingua: String,
        valutazione: Number,
    }


};
</script>

<template>
    <div class="col d-grid gap-3 my-2">

        <div class="box text-ceter">
            <h3 class="p-2 text-white text-ceter">{{ titolo }}</h3>
            <h3 class="p-2 text-white text-ceter">{{ titoloCer }}</h3>
            <h3 class="p-2 text-white text-ceter">{{ lingua }}</h3>
            <h3 class="p-2 text-white text-ceter">{{ valutazione }}</h3>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>