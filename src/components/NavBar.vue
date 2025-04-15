<template>
  <v-app-bar class="px-4 border-b border-gray-800 bg-black">
    <div class="flex items-center">
      <span class="gradient-text font-medium text-lg md:text-xl">moviebox</span>
      <span class="text-[#9CA3AF] text-lg md:text-xl">Admin</span>
    </div>

    <v-tabs
      v-model="activeTab"
      color="#FF6B81"
      class="ml-4 md:ml-8 overflow-x-auto"
      slider-size="2"
    >
      <v-tab
        v-for="item in menuItems"
        :key="item.title"
        :value="item.value"
        class="text-[#9CA3AF] hover:text-gray-200 text-xs md:text-sm transition-colors duration-200 min-w-fit px-2 md:px-4"
        :class="{ 'text-white': activeTab === item.value }"
      >
        {{ item.title }}
      </v-tab>
    </v-tabs>

    <v-spacer></v-spacer>

    <div class="flex items-center gap-2 md:gap-4">
      <v-btn
        icon
        size="small"
        class="text-[#9CA3AF] hover:text-gray-200 transition-colors duration-200"
      >
        <v-icon>mdi-cog-outline</v-icon>
      </v-btn>

      <div class="relative">
        <v-btn
          icon
          size="small"
          class="text-[#9CA3AF] hover:text-gray-200 transition-colors duration-200"
        >
          <v-icon>mdi-bell-outline</v-icon>
        </v-btn>
        <span class="absolute -top-1 -right-1 bg-gradient-to-r from-pink-500 via-red-500 to-rose-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center">
          2
        </span>
      </div>

      <v-avatar
        size="28"
        class="cursor-pointer hidden sm:flex"
      >
        <v-img src="https://i.pravatar.cc/300" class="rounded-full"></v-img>
      </v-avatar>
    </div>
  </v-app-bar>
</template>