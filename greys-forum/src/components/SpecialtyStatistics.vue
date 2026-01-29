<script>
export default {
  props: {
    characters: {
      type: Array,
      required: true
    }
  },
  computed: {
    specialtyStatistics() {
      const specialties = ['Cardio', 'General', 'Pediatric']
      const statistics = {
        Cardio: 0,
        General: 0,
        Pediatric: 0
      }

      this.characters.forEach(character => {
        specialties.forEach(specialty => {
          if (character.specialty.indexOf(specialty) > -1) {
            statistics[specialty] += 1
          }
        })
      })

      return statistics
    }
  }
}
</script>

<template>
    <h2>Statistics</h2>
    <ul>
        <li 
        v-for="(stat, type) in specialtyStatistics"
        :key="`specialty-${stat}-${type}`"
        >{{ type }}: {{ stat }}</li>
    </ul>
</template>