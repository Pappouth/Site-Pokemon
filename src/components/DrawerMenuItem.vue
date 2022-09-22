<template>
    <q-item :to="to" exact>
        <q-item-section v-if="type == 'sidebar'" avatar>
            <q-icon :name="iconName" />
        </q-item-section>
        <q-item-section>
            <q-item-label>{{ name }}</q-item-label>
        </q-item-section>
    </q-item>
</template>

<style></style>

<script>
export default {
    name: "DrawerMenuItem",
    props: { type: String, iconName: String, name: String, to: String },
};
</script>
