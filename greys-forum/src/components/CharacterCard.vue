<script>
export default {
    props: {
        character: {
            type: Object,
            required: true,
        }
    },
    emits: ['favourite'],
    methods: {
        favouriteCharacter(favourite) {
            this.$emit('favourite', this.character);
        }
    }
}
</script>

<template>
    <div>
        <p>{{ character.name }}</p>
        <button @click="favouriteCharacter">⭐️ Favourite</button>
    </div>
</template>