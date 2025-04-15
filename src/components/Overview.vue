<template>
    <div class="p-6">
      <div class="flex justify-between items-center mb-8">
        <h1 class="text-2xl font-medium">Overview</h1>
        <div class="flex gap-4">
          <v-btn variant="outlined" prepend-icon="mdi-filter-variant">
            Filter
          </v-btn>
          <v-btn variant="outlined" prepend-icon="mdi-export">
            Export
          </v-btn>
        </div>
      </div>
  
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <!-- User Logins Chart -->
        <v-card class="p-4 rounded-lg">
          <div class="flex justify-between items-center mb-4">
            <h2 class="text-lg font-medium">Today's user logins</h2>
            <v-btn icon size="small">
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </div>
          <div class="h-[300px] flex justify-center items-center">
            <Doughnut :data="donutData" :options="donutOptions" />
          </div>
          <div class="text-center mt-12">
            <v-btn 
              variant="outlined" 
              class="rounded-full px-6 py-2 text-gray-700 border-[#E0E0E0] hover:bg-gray-50"
            >
              View full report
            </v-btn>
          </div>
        </v-card>
  
        <!-- Watch Time Chart -->
        <v-card class="p-4 rounded-lg">
          <div class="flex justify-between items-center mb-4">
            <div>
              <h2 class="text-lg font-medium">Average watch time</h2>
              <p class="text-sm text-gray-500">This tracks the average watch by users every month</p>
            </div>
            <v-btn icon size="small">
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </div>
          <div class="flex justify-end gap-2 mb-4">
            <v-chip size="small" variant="outlined" class="text-xs ">0 - 1000</v-chip>
            <v-chip size="small" variant="outlined" class="text-xs">1000 - 10,000</v-chip>
          </div>
          <div class="h-[300px]">
            <Line :data="lineData" :options="lineOptions" />
          </div>
        </v-card>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import { Doughnut, Line } from 'vue-chartjs'
  import {
    Chart as ChartJS,
    ArcElement,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend,
    Filler
  } from 'chart.js'
  
  ChartJS.register(
    ArcElement,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend,
    Filler
  )
  
  const gradients = {
    blue: {
      start: '#35C3F3',
      end: '#8B9FE8'
    },
    purple: {
      start: '#8B9FE8',
      end: '#E681D8'
    },
    pink: {
      start: '#E681D8',
      end: '#FFA9A4'
    },
    coral: {
      start: '#FFA9A4',
      end: '#FED2CE'
    }
  }
  
  const createGradient = (context, start, end) => {
    const gradient = context.createLinearGradient(0, 0, 200, 0)
    gradient.addColorStop(0, start)
    gradient.addColorStop(1, end)
    return gradient
  }
  
  const donutData = {
    labels: ['0 - 1,000', '1,000 - 10,000', '10,000 - 100,000', '100,000 - 1,000,000'],
    datasets: [{
      data: [30, 25, 25, 20],
      backgroundColor: (context) => {
        const chart = context.chart
        const {ctx} = chart
        return [
          createGradient(ctx, gradients.blue.start, gradients.blue.end),
          createGradient(ctx, gradients.purple.start, gradients.purple.end),
          createGradient(ctx, gradients.pink.start, gradients.pink.end),
          createGradient(ctx, gradients.coral.start, gradients.coral.end)
        ]
      },
      borderWidth: 0
    }]
  }
  
  const donutOptions = {
    responsive: true,
    maintainAspectRatio: false,
    plugins: {
      legend: {
        position: 'right',
        align: 'center',
        labels: {
          usePointStyle: true,
          padding: 20,
          font: {
            size: 12,
            family: "'Roboto', sans-serif"
          },
          color: '#000000'
        }
      }
    },
    cutout: '80%'
  }
  
  const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
  
  const lineData = {
    labels: months,
    datasets: [
      {
        label: 'Watch time',
        data: generateRandomData(12, 200, 500),
        borderColor: (context) => {
          const chart = context.chart
          const {ctx} = chart
          const gradient = ctx.createLinearGradient(0, 0, 300, 0)
          gradient.addColorStop(0, '#35C3F3')
          gradient.addColorStop(0.5, '#8B9FE8')
          gradient.addColorStop(1, '#E681D8')
          return gradient
        },
        backgroundColor: (context) => {
          const chart = context.chart
          const {ctx} = chart
          const gradient = ctx.createLinearGradient(0, 0, 0, 300)
          gradient.addColorStop(0, 'rgba(53, 195, 243, 0.2)')
          gradient.addColorStop(1, 'rgba(230, 129, 216, 0.05)')
          return gradient
        },
        tension: 0.4,
        fill: true
      }
    ]
  }
  
  const lineOptions = {
    responsive: true,
    maintainAspectRatio: false,
    plugins: {
      legend: {
        display: false
      }
    },
    scales: {
      y: {
        beginAtZero: true,
        grid: {
          color: 'rgba(0, 0, 0, 0.1)',
          drawBorder: false
        },
        ticks: {
          callback: value => value + 'k',
          stepSize: 250,
          color: '#000000'
        }
      },
      x: {
        grid: {
          display: false
        },
        ticks: {
          color: '#000000'
        }
      }
    }
  }
  
  function generateRandomData(count, min, max) {
    return Array.from({ length: count }, () => 
      Math.floor(Math.random() * (max - min + 1)) + min
    )
  }
  </script>