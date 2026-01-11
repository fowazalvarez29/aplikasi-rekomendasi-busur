<template>
  <div class="flex">

    <div
      v-if="sidebarOpen"
      class="fixed inset-0 bg-black/40 z-30 md:hidden"
      @click="sidebarOpen = false"
    ></div>

    <!-- SIDEBAR -->
    <aside
      :class="[
        'fixed top-0 left-0 h-screen bg-white shadow-lg p-6 flex flex-col z-40 transform transition-all duration-300',
        'w-64',
        sidebarOpen ? 'translate-x-0' : '-translate-x-full md:translate-x-0'
      ]"
    >

      <!-- Header sidebar -->
      <div class="flex justify-between items-center mb-10">
        <div class="flex items-center gap-3">
         <img :src="logo" class="w-12 h-12 object-contain" />
          <h2 class="text-lg font-bold text-[#0A5C44] leading-tight">
            Rekomendasi Busur Pemanah<br/> Pemula
          </h2>
        </div>

        <!-- Tombol close -->
        <button
          class="md:hidden text-2xl text-[#0A5C44] mb-20"
          @click="sidebarOpen = false"
        >
          ✕
        </button>
      </div>

      <!-- MENU -->
      <nav class="flex flex-col gap-3">
        <button
          @click="setTab('manual')"
          :class="tabClass('manual')"
        >
          Input Data
        </button>

        <button
          @click="setTab('excel')"
          :class="tabClass('excel')"
        >
          Upload Dokumen
        </button>
        <button
          @click="setTab('template')"
          :class="tabClass('template')"
        >
          Template Dokumen
       </button>

       <button
        @click="setTab('panduan')"
        :class="tabClass('panduan')"
      >
        Panduan Pengguna
      </button>

      </nav>
    </aside>

    <!-- MAIN CONTENT -->
    <main class="flex-1 md:ml-64 p-6 md:p-10">

      <!-- BUTTON TO OPEN SIDEBAR (Mobile) -->
      <button
        class="md:hidden mb-6 text-3xl text-[#0A5C44]"
        @click="sidebarOpen = true"
      >
        ☰
      </button>

      <!-- JUDUL -->
      <div>
        <h1 class="text-4xl md:text-5xl font-bold text-[#0A5C44] tracking-wide text-center">
          Rekomendasi Busur Panah
        </h1>
        <p class="mt-3 text-lg text-[#0A5C44] text-center">
          Isi data siswa atau upload dokumen (excel) untuk mendapatkan analisis dan rekomendasi peralatan
        </p>
      </div>

      <!-- CONTENT -->
      <div class="mt-10">
        <FormInput
          v-if="activeTab === 'manual'"
          @hasilManual="manualResult = $event"
        />
        <UploadExcel
          v-if="activeTab === 'excel'"
          @hasilExcel="excelResult = $event"
        />
        <DownloadTemplate
          v-if="activeTab === 'template'"
        />
        <UserGuide
          v-if="activeTab === 'panduan'"
        />

      </div>

      <!-- HASIL -->
      <div v-if="activeTab === 'manual'">
        <ResultCard v-if="manualResult" :data="manualResult" />
      </div>

      <div v-if="activeTab === 'excel'">
        <ResultExcel v-if="excelResult && excelResult.length > 0" 
                    :results="excelResult" />
      </div>

      <!-- === FOOTER === -->
      <footer class="mt-16 py-6 text-center text-gray-600 text-sm border-t flex flex-col items-center gap-3">

        <p>
          © {{ new Date().getFullYear() }} Aplikasi Rekomendasi Busur Pemanah - By FowazDev
        </p>
      </footer>


    </main>
  </div>
</template>

<script setup>
import { ref } from "vue"
import FormInput from "./components/FormInput.vue"
import UploadExcel from "./components/UploadExcel.vue"
import ResultCard from "./components/ResultCard.vue"
import ResultExcel from "./components/ResultExcel.vue"
import DownloadTemplate from "./components/DownloadTemplate.vue"  
import UserGuide from "./components/UserGuide.vue"

const activeTab = ref("manual")
const manualResult = ref(null)
const excelResult = ref(null)

// Sidebar state (mobile)
const sidebarOpen = ref(false)

// Handle tab switch
const setTab = (tab) => {
  activeTab.value = tab
  sidebarOpen.value = false

  if (tab === "manual") {
    excelResult.value = null
  } else if (tab === "excel") {
    manualResult.value = null
  }
}

const tabClass = (tab) => {
  return [
    'text-left px-4 py-2 rounded-lg font-medium transition',
    activeTab.value === tab
      ? 'bg-[#0A5C44] text-white'
      : 'text-gray-700 hover:bg-gray-100'
  ]
}

import logo from "@/assets/logo.png"

</script>



