<template>
    <q-card>
        <q-card-section class="text-center">
            <!-- info générales -->
            <q-img
                :src="imageSource"
                style="height: 100px; width: 100px"
            />
            <q-item class="text-h4 justify-center">{{ name }}</q-item>
            <q-item class="text-h6 justify-center">n°{{ numero }}</q-item>

            <!-- Types -->
            <div style="display: flex; flex-direction: row; justify-content: center; align-items: center">
                <q-item
                    style="display: flex; flex-direction: column; align-items: center;"
                    class="text-h6"
                    v-for="pokemonType in types"
                    :key="pokemonType.id"
                >
                    <img
                        :src="pokemonType['image']"
                        style="height: 25px; width:25px;"
                    />
                    <q-item-label>{{ pokemonType['name'] }}</q-item-label>
                </q-item>
            </div>
        </q-card-section>
    </q-card>
</template>

<script>
export default {
    name: "PokemonCard",
    props: { imageSource: String, name: String, numero: Number, types: Object },
    // data() {
    //     return {
    //         typesArr: []
    //     }
    // },
    // methods: {
    //     loadTypes() {
    //         this.types.forEach((typeInfo) => {
    //             const typeName = Object.values(typeInfo)[0];
    //             const typeImage = Object.values(typeInfo)[1];

    //             this.typesArr.push([typeName, typeImage]);
    //         });
    //         console.log(this.typesArr);
    //     }
    // },
    // mounted() {
    //     this.loadTypes();
    // }
}
</script>