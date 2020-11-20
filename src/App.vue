<template>
  <div id="app">
    <div class="container-fluid text-white" style="position: relative;">
      <TheHeader
        :selectedLength="selectedCharacters.length"
        @on-download="download"
        @on-reset="reset"
      />
      <div class="row">
        <CharacterItem
          :key="index"
          v-for="(character, index) in characters"
          @on-select-character="selectCharacter"
          :character="character"
        />
      </div>
      <TheFooter
        :currentPage="currentPage"
        :lastPage="lastPage"
        @on-next-page="nextPage"
        @on-previous-page="previousPage"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import TheHeader from "./components/TheHeader";
import TheFooter from "./components/TheFooter";
import CharacterItem from "./components/CharacterItem";

export default {
  name: "App",
  data: function() {
    return {
      characters: [],
      selectedCharacters: [],
      currentPage: 1,
      lastPage: 1,
    };
  },
  components: {
    TheHeader,
    TheFooter,
    CharacterItem,
  },
  mounted() {
    this.fetchCharacters(this.currentPage);
  },
  methods: {
    download() {
      let csv = this.convertToCSV(this.selectedCharacters);
      let csvContent = "data:text/csv;charset=utf-8," + csv;
      var encodedUri = encodeURI(csvContent);
      window.open(encodedUri);
    },
    reset() {
      for (const i in this.characters) this.characters[i].isSelected = false;
      this.selectedCharacters = [];
    },
    nextPage() {
      console.log(this.selectedCharacters);
      if (this.currentPage == this.lastPage) return;
      this.currentPage += 1;
      this.fetchCharacters(this.currentPage);
    },
    previousPage() {
      if (this.currentPage == 1) return;
      this.currentPage -= 1;
      this.fetchCharacters(this.currentPage);
    },
    //In large application, we will vuex for stat management
    async fetchCharacters(page) {
      try {
        let response = await axios.get(
          "https://swapi.dev/api/people/?page=" + page
        );
        this.characters = [];
        for (const element of response.data.results) {
          element.isSelected = this.selectedCharacters.find(
            (item) => item.name === element.name
          );

          this.characters.push(element);
        }
        this.lastPage = parseInt(response.data.count / 10);
      } catch (error) {
        console.log(error);
      }
    },

    // ====================  Callbacks from children componenets  ========================================  //
    selectCharacter(character) {
      //If character already selected, we should unselect it
      if (
        this.selectedCharacters.find((item) => item.name === character.name)
      ) {
        character.isSelected = false;
        this.selectedCharacters = this.selectedCharacters.filter(
          (item) => item.name !== character.name
        );
        return;
      }
      console.log(this.selectedCharacters);
      if (this.selectedCharacters.length == 3) {
        alert("Maximum number for characters selection is 3");
        return;
      }
      character.isSelected = true;
      this.selectedCharacters.push(character);
    },
    //Will move to Utils class in large application
    convertToCSV(arr) {
      const array = [Object.keys(arr[0])].concat(arr);
      return array
        .map((it) => {
          return Object.values(it).toString();
        })
        .join("\n");
    },
  },
};
</script>

<style></style>
