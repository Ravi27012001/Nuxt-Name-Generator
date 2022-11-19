<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data";
 
interface Namee {
  gender: string;
  popularity: string;
  length: string;
}
const choise = reactive<Namee>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.LONG,
});

const show = ref(false);
const ComputedList = () => {
  show.value = true;

  const filteredList = names
    .filter((name) => name.gender === choise.gender)
    .filter((name) => name.popularity === choise.popularity)
    .filter((name) => {
      if (choise.length === Length.ALL) return true;
      else {
        return name.length === choise.length;
      }
    });

  generatedName.value = filteredList.map((name) => {
    return name.name;
  });
};
const generatedName = ref<string[]>([]);
</script>


<template>
  <div class="">
    <h1 class="text-[40px] font-bold text-center text-red-600 font-serif">
      Baby Name-Generator
    </h1>
    <div class="bg-yellow-200 text-[25px] text-center block w-1/3 m-auto p-6">
      <p class="text-red-600 font-bold font-serif text-[35px]">
        Select the options
      </p>
      <div class="border-2 border-red-400 rounded-xl">
        <div class="pb-2">Select the gender</div>
        <div class="flex justify-around">
          <button
            class="option rounded-bl-lg"
            :class="choise.gender === Gender.BOY && 'selected'"
            @click="choise.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="option"
            :class="choise.gender === Gender.GIRL && 'selected'"
            @click="choise.gender = Gender.GIRL"
          >
            Girl
          </button>
          <button
            class="option rounded-br-lg"
            :class="choise.gender === Gender.UNISEX && 'selected'"
            @click="choise.gender = Gender.UNISEX"
          >
            Unisex
          </button>
        </div>
      </div>
      <div class="border-2 border-red-400 rounded-xl mt-1">
        <div class="pb-2">Select the Name's Popularity</div>
        <div class="flex justify-around">
          <button
            class="options rounded-bl-lg"
            :class="choise.popularity === Popularity.TRENDY && 'selected'"
            @click="choise.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
            class="options rounded-br-lg"
            :class="choise.popularity === Popularity.UNIQUE && 'selected'"
            @click="choise.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div class="border-2 border-red-400 rounded-xl mt-1">
        <div class="pb-2">Select the Name's length</div>
        <div class="flex justify-around">
          <button
            class="option rounded-bl-lg"
            :class="choise.length === Length.LONG && 'selected'"
            @click="choise.length = Length.LONG"
          >
            Long
          </button>
          <button
            class="option"
            :class="choise.length == Length.ALL && 'selected'"
            @click="choise.length = Length.ALL"
          >
            All
          </button>
          <button
            class="option rounded-br-lg"
            :class="choise.length == Length.SHORT && 'selected'"
            @click="choise.length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>
      <button
        class="
          bg-blue-600
          text-white
          p-2
          mt-3
          text-[25px]
          rounded-md
          font-serif font-bold
          hover:bg-blue-700
        "
        @click="ComputedList()"
      >
        Submit
      </button>
    </div>
    <div class="flex flex-row text-center m-auto mt-4 gap-3 w-96 align-middle flex-wrap justify-center">
      <div
        v-show="show"
        v-for="item in generatedName"
        :key="item"
        class="border-2 border-red-500 p-1 px-2 font-serif text-[25px] font-semibold rounded-md"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.option {
  background-color: white;
  outline: 2px solid red;
  border: none;
  padding: 5px;
  width: 200px;
  font-size: 23px;
  color: rgb(24, 52, 120);
  cursor: pointer;
  font-weight: 400;
}
.options {
  background-color: white;
  outline: 2px solid red;
  border: none;
  padding: 5px;
  width: 300px;
  font-size: 23px;
  color: rgb(24, 52, 120);
  cursor: pointer;
}
.selected {
  background-color: rgb(220, 63, 63);
  color: white;
}
</style>