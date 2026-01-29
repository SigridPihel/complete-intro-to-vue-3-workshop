<script>
import SpecialtyStatistics from './components/SpecialtyStatistics.vue';
import CharacterCard from './components/CharacterCard.vue';
import BaseLayout from './components/BaseLayout.vue';

export default {
  components: {
    SpecialtyStatistics,
    CharacterCard,
    BaseLayout
  },
  data: () => ({
    favouritesList: [],
    listOfCharacters: [
      {
          name: "Meredith",
          specialty: ['General']
      }, {
          name: "Chistina",
          specialty: ['Cardio']
      }, {
          name: "Alex",
          specialty: ['Pediatric']
      }, {
          name: "Bailey",
          specialty: ['General']
      }
    ],
    favouritesList: [],
    newCharacter: {
      name: '',
      specialty: []
    }
  }),
  methods: {
    addNewCharacter() {
      this.listOfCharacters.push(this.newCharacter)
      this.newCharacter = { name: '' }
    },
    addFavouriteCharacter(payload) {
      this.favouritesList.push(payload);
    }
  }
}
</script>

<template>
  <BaseLayout>
    <template v-slot:one>
      <h2>New Character</h2>
      <pre>
        {{ newCharacter }}
      </pre>
      <label for="character-name">Name: </label>
      <input 
        type="text" 
        v-model="newCharacter.name"
        @keyup.enter="addNewCharacter"
      />
    </template>
  </BaseLayout>
  <h1>My Favourite TV show</h1>

<SpecialtyStatistics :characters="listOfCharacters" />
  
<h2>Characters</h2>
  <p v-if="listOfCharacters.length === 0">There are no characters in the show! 🥹</p>
  <ul v-else>
      <li 
      v-for="(character, index) in listOfCharacters"
      :key="`character-${index}`"
      >
      <CharacterCard :character="character" @favourite="addFavouriteCharacter"/>
      </li>
  </ul>
  <p>
      Characters in the show:
      <span 
      v-for="(character, index) in listOfCharacters"
      :key="`comma-list-character-${index}`"
      >
      {{ character.name }} {{ index === listOfCharacters.length - 1 ? '' : ', '}}
      </span>
  </p>

  <h2>My Favourite Characters</h2>
  <ul v-if="favouritesList.length > 0">
      <li 
      v-for="(character, index) in favouritesList"
      :key="`favourite-character-${index}`"
      >
      {{ character.name }}
      </li>
  </ul>
  <p v-else>No favourite characters!</p>
</template>

