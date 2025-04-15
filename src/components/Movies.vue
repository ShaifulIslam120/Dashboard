<template>
    <div class="p-6">
      <div class="flex justify-between items-center mb-6">
        <div>
          <h1 class="text-xl font-medium">Upcoming movie premieres</h1>
          <p class="text-gray-500 text-sm">Keep track of the upcoming movie premieres</p>
        </div>
        <div class="relative w-[280px]">
          <v-text-field
            v-model="search"
            prepend-inner-icon="mdi-magnify"
            placeholder="Search"
            variant="outlined"
            density="compact"
            hide-details
            class="search-field"
            bg-color="white"
          />
        </div>
      </div>
  
      <v-card class="rounded-lg">
        <v-table>
          <thead class="bg-[#E0E0E080]">
            <tr>
              <th class="text-left pl-6">
                Name
                <v-icon size="small" class="ml-1">mdi-arrow-down</v-icon>
              </th>
              <th class="text-left">Category</th>
              <th class="text-left">Watchlists</th>
              <th class="text-left">Owner</th>
              <th class="text-left">Premier Date</th>
              <th class="text-right pr-6"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="movie in movies" :key="movie.name" class="border-b">
                <td class="py-4 pl-6">
  <div class="flex items-center gap-3">
    <div class="w-12 h-12 overflow-hidden rounded-full">
      <v-img 
        :src="movie.image" 
        width="40" 
        height="40" 
        class="rounded-full"
        cover
      />
    </div>
    <span class="font-medium">{{ movie.name }}</span>
  </div>
</td>   
              <td>
                <div class="flex gap-2">
                  <v-chip
                    v-for="category in movie.categories"
                    :key="category"
                    size="small"
                    class="text-xs bg-[#EEF2FF] text-[#4755A8BF] bg-[#4F46E51B]  px-3 font-medium"
                    variant="flat"
                    density="comfortable"
                  >
                    {{ category }}
                  </v-chip>
                  <v-chip
                    v-if="movie.moreCategories"
                    size="small"
                    class="text-xs bg-[#EEF2FF] text-[#4755A8BF] px-3 font-medium "
                    variant="flat"
                    density="comfortable"
                  >
                    +{{ movie.moreCategories }} more
                  </v-chip>
                </div>
              </td>
              <td>{{ movie.watchlists.toLocaleString() }}</td>
              <td>{{ movie.owner }}</td>
              <td>{{ movie.premierDate }}</td>
              <td class="text-right pr-6">
                <v-btn
                  variant="outlined"
                  size="small"
                  class="rounded-lg px-4"
                >
                  View
                </v-btn>
              </td>
            </tr>
          </tbody>
        </v-table>
        <div class="text-right  bg-[#E0E0E080] p-2">
        <v-btn
          variant="outlined"
          class="bg-gray-50 border border-gray-200 rounded-lg px-6 text-gray-700 hover:bg-gray-100 font-bold"
        >
          View all upcoming premieres
        </v-btn>
      </div>
      </v-card>
  
      
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import  Avengers from "../assets/Avngers.png"
  import Moonlight from "../assets//Moonlight.png"
  
  const search = ref('')
  
  const movies = [
    {
      name: 'Avengers Black Widow',
      image: Avengers,
      categories: ['ACTION', 'THRILLER'],
      watchlists: 389234,
      owner: 'Sony Entertainment',
      premierDate: '21th May, 2022'
    },
    {
      name: 'Moonlight',
      image: Moonlight,
      categories: ['TRUE STORY'],
      moreCategories: 2,
      watchlists: 5893,
      owner: 'A24 and Plan B Entertainment',
      premierDate: '15th August, 2022'
    },
    {
      name: 'Grimsby',
      image: '/movies/grimsby.jpg',
      categories: ['COMEDY', 'CRIME'],
      watchlists: 200901,
      owner: 'Sony Entertainment',
      premierDate: '5th October, 2022'
    },
    {
      name: 'Spider Man - No way home',
      image: '/movies/spiderman.jpg',
      categories: ['ACTION', 'THRILLER'],
      watchlists: 509262,
      owner: 'Sony Entertainment',
      premierDate: '25th December, 2022'
    }
  ]
  </script>