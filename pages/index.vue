<template>
  <nav class="bg-white/90 backdrop-blur-md border-b border-gray-200 shadow-lg p-4 md:p-6">
    <div class="max-w-7xl mx-auto flex items-center justify-between">
      <!-- Logo Section -->
      <div class="flex items-center gap-3">
        <img src="../assets/images/1.png" alt="Logo" class="h-10 w-10" />
        <span class="text-xl md:text-2xl font-bold text-blue-600">
          แพลตฟอร์มแสดงผลและจัดการพลังงานผ่านระบบ IOT
        </span>
      </div>

      <!-- Navigation Links -->
     <div class="hidden md:flex gap-6">
        <router-link
          to="/"
          class="font-medium text-gray-700 hover:text-indigo-600 transition-all duration-300"
          :class="{ 'text-indigo-700 font-bold underline': $route.path === '/' }"
        >
          หน้าหลัก
        </router-link>
        <router-link
          to="/monthly-summary"
          class="font-medium text-gray-700 hover:text-indigo-600 transition-all duration-300"
          :class="{ 'text-indigo-700 font-bold underline': $route.path === '/monthly-summary' }"
        >
          รายละเอียด
        </router-link>
      </div>

      
    </div>

    
  </nav>

   <div class="min-h-screen bg-gradient-to-tr from-blue-100 via-indigo-200 to-purple-100 p-4 md:p-8 animate-fadeIn">
  <h2 class="text-center text-3xl md:text-4xl font-bold text-indigo-900 mb-8 animate-slideUp" style="animation-delay: 0.2s;">
    หน้าแสดงข้อมูลจาก Sensor
  </h2>

  <div class="bg-white/90 backdrop-blur-md rounded-2xl shadow-2xl p-6 md:p-8 mb-8 max-w-4xl mx-auto animate-slideUp" style="animation-delay: 0.4s;">
    <div class="flex justify-between items-center mb-6 border-b border-indigo-200 pb-4">
      <h3 class="text-xl font-bold text-indigo-800">ข้อมูลจากเซนเซอร์แบบเรียลไทม์</h3>
      <div class="flex items-center gap-2">
        <span class="relative flex h-3 w-3">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
          <span class="relative inline-flex rounded-full h-3 w-3 bg-green-500"></span>
        </span>
        <span class="font-semibold text-green-600">ออนไลน์</span>
      </div>
    </div>
    
    <div class="grid grid-cols-2 md:grid-cols-3 gap-4 md:gap-6 text-center">
      <div class="bg-indigo-50/60 rounded-xl p-4 shadow-md hover:shadow-lg hover:bg-indigo-100/70 transition-all duration-300 transform hover:-translate-y-1">
        <p class="text-indigo-700 font-semibold">แรงดันไฟฟ้า</p>
        <p class="text-2xl font-bold text-gray-900">{{ liveData.voltage }} <span class="text-lg font-medium text-gray-600">V</span></p>
      </div>
      <div class="bg-indigo-50/60 rounded-xl p-4 shadow-md hover:shadow-lg hover:bg-indigo-100/70 transition-all duration-300 transform hover:-translate-y-1">
        <p class="text-indigo-700 font-semibold">กระแสไฟฟ้า</p>
        <p class="text-2xl font-bold text-gray-900">{{ liveData.current }} <span class="text-lg font-medium text-gray-600">A</span></p>
      </div>
      <div class="bg-indigo-50/60 rounded-xl p-4 shadow-md hover:shadow-lg hover:bg-indigo-100/70 transition-all duration-300 transform hover:-translate-y-1">
        <p class="text-indigo-700 font-semibold">กำลังไฟฟ้า</p>
        <p class="text-2xl font-bold text-gray-900">{{ liveData.power }} <span class="text-lg font-medium text-gray-600">W</span></p>
      </div>
      <div class="bg-indigo-50/60 rounded-xl p-4 shadow-md hover:shadow-lg hover:bg-indigo-100/70 transition-all duration-300 transform hover:-translate-y-1">
        <p class="text-indigo-700 font-semibold">พลังงานสะสม</p>
        <p class="text-2xl font-bold text-gray-900">{{ liveData.energy }} <span class="text-lg font-medium text-gray-600">kWh</span></p>
      </div>
      <div class="bg-indigo-50/60 rounded-xl p-4 shadow-md hover:shadow-lg hover:bg-indigo-100/70 transition-all duration-300 transform hover:-translate-y-1">
        <p class="text-indigo-700 font-semibold">ความถี่</p>
        <p class="text-2xl font-bold text-gray-900">{{ liveData.frequency }} <span class="text-lg font-medium text-gray-600">Hz</span></p>
      </div>
      <div class="bg-indigo-50/60 rounded-xl p-4 shadow-md hover:shadow-lg hover:bg-indigo-100/70 transition-all duration-300 transform hover:-translate-y-1">
        <p class="text-indigo-700 font-semibold">ตัวประกอบกำลัง</p>
        <p class="text-2xl font-bold text-gray-900">{{ liveData.pf }}</p>
      </div>
    </div>
  </div>


    <!-- Historical Sensor Data Table -->
    <div class="bg-white/80 backdrop-blur-md rounded-xl shadow-lg p-6 max-w-5xl mx-auto">
      <h3 class="text-center text-xl font-bold text-gray-800 mb-6">ข้อมูลประวัติการวัด (10 รายการล่าสุด)</h3>
      <div class="overflow-x-auto">
        <table class="table-auto w-full">
          <thead>
            <tr class="bg-indigo-100 font-semibold text-gray-800">
              <th class="text-left px-4 py-2">เวลาที่บันทึก</th>
              <th class="text-left px-4 py-2">แรงดันไฟฟ้า (V)</th>
              <th class="text-left px-4 py-2">กระแสไฟฟ้า (A)</th>
              <th class="text-left px-4 py-2">กำลังไฟฟ้า (W)</th>
              <th class="text-left px-4 py-2">พลังงานสะสม (kWh)</th>
              <th class="text-left px-4 py-2">ความถี่ (Hz)</th>
              <th class="text-left px-4 py-2">ตัวประกอบกำลัง</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="record in historicalData.slice(-10)" :key="record.timestamp" class="odd:bg-white even:bg-gray-400">
              <td class="px-4 py-2">{{ formatTimestamp(record.timestamp) }}</td>
              <td class="px-4 py-2">{{ record.voltage }} V</td>
              <td class="px-4 py-2">{{ record.current }} A</td>
              <td class="px-4 py-2">{{ record.power }} W</td>
              <td class="px-4 py-2">{{ record.energy }} kWh</td>
              <td class="px-4 py-2">{{ record.frequency }} Hz</td>
              <td class="px-4 py-2">{{ record.pf }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { format } from 'date-fns';
import { th } from 'date-fns/locale';

const liveData = ref({
  voltage: 0,
  current: 0,
  power: 0,
  energy: 0,
  frequency: 0,
  pf: 0,
});

const historicalData = ref([]);

// Format timestamp to Thai time and format
const formatTimestamp = (timestamp: string) => {
  return format(new Date(timestamp), "dd MMM yyyy HH:mm:ss", { locale: th });
};

// Fetch the latest live data
const fetchLiveData = async () => {
  try {
    const response = await fetch('http://localhost:4000/get-latest-sensor-data');
    liveData.value = await response.json();
  } catch (error) {
    console.error("Error fetching live data:", error);
  }
};

// Fetch historical data
const fetchHistoricalData = async () => {
  try {
    const response = await fetch('http://localhost:4000/get-sensor-history?limit=10');
    historicalData.value = await response.json();
  } catch (error) {
    console.error("Error fetching historical data:", error);
  }
};

// Fetch live data and historical data together
const fetchAllData = async () => {
  await fetchLiveData();
  await fetchHistoricalData();
};

// Fetch data on mount and set up periodic updates for live data
onMounted(() => {
  fetchAllData(); // Fetch both live data and historical data when mounted

  // Update both live data and historical data every second
  setInterval(fetchAllData, 1000);
});
</script>

<style scoped>
.table-auto thead tr th {
  @apply bg-indigo-100 text-gray-800 px-4 py-2;
}

.table-auto tbody tr td {
  @apply px-4 py-2 text-gray-800;
}

.table-auto tbody tr:nth-child(odd) {
  @apply bg-white;
}

.table-auto tbody tr:nth-child(even) {
  @apply bg-gray-50;
}
</style>