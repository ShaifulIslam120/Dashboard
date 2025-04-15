<template>
    <div class="p-6">
      <div class="flex justify-between items-center mb-6">
        <div>
          <h1 class="text-xl font-medium">Trending movies</h1>
          <p class="text-gray-500 text-sm">Keep track of the trending movies on moviebox</p>
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
          <thead class="bg-gray-50">
            <tr>
              <th class="text-left pl-6">
                Name
                <v-icon size="small" class="ml-1">mdi-arrow-down</v-icon>
              </th>
              <th class="text-left">Category</th>
              <th class="text-left">Watchlists</th>
              <th class="text-left">Streams</th>
              <th class="text-left">Release Date</th>
              <th class="text-right pr-6"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="movie in movies" :key="movie.name" class="border-b">
                <td class="py-4 pl-6">
  <div class="flex items-center gap-3">
    <div class="w-10 h-10 rounded-full overflow-hidden flex items-center justify-center">
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
                    class="text-xs bg-[#4F46E51B] text-[#4755A8BF] px-3 font-medium"
                    variant="flat"
                    density="comfortable"
                  >
                    {{ category }}
                  </v-chip>
                  <v-chip
                    v-if="movie.moreCategories"
                    size="small"
                    class="text-xs bg-[#4F46E51B] text-[#4755A8BF] px-3 font-medium"
                    variant="flat"
                    density="comfortable"
                  >
                    +{{ movie.moreCategories }} more
                  </v-chip>
                </div>
              </td>
              <td>{{ movie.watchlists.toLocaleString() }}</td>
              <td>{{ movie.streams.toLocaleString() }}</td>
              <td>{{ movie.releaseDate }}</td>
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
  import moonlight from "../assets/Moonlight.png"
  
  const search = ref('')
  
  const movies = [
    {
      name: 'Moonlight',
      image: moonlight,
      categories: ['TRUE STORY'],
      moreCategories: 2,
      watchlists: 5893,
      streams: 24512232,
      releaseDate: '4th July, 2012'
    },
    {
      name: 'Grimsby',
      image: '/movies/grimsby.jpg',
      categories: ['COMEDY', 'CRIME'],
      watchlists: 200901,
      streams: 4164476,
      releaseDate: '21th May, 2003'
    },
    {
      name: 'Spider Man - Far from Home',
      image: '/movies/spiderman.jpg',
      categories: ['ACTION', 'THRILLER'],
      watchlists: 389234,
      streams: 13043145,
      releaseDate: '14th June, 2012'
    }
  ]
  </script>