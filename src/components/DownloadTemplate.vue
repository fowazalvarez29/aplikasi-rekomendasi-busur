<template>
  <div class="bg-white p-6 rounded-2xl border shadow-sm">

    <label class="font-medium text-[#0A5C44] text-xl">Download Template Dokumen (Excel)</label>
    <p class="text-xs text-gray-500 mt-1 leading-relaxed">
      Silakan unduh file template dokumen (.xlsx) berikut untuk digunakan sebagai acuan 
      pengisian data. Pastikan seluruh kolom yang tersedia diisi sesuai format yang telah 
      ditentukan agar sistem dapat memproses data dengan benar.
    </p>

    <!-- BOX CATATAN -->
    <div class="mt-4 p-4 rounded-xl border border-yellow-300 bg-yellow-50">
      <p class="text-sm font-medium text-yellow-800 flex items-start gap-2">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 text-yellow-700 mt-0.5"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L4.207 16c-.77 1.333.192 3 1.732 3z" />
        </svg>
        Pastikan tidak mengubah nama kolom pada template Excel agar file tidak dianggap
        rusak atau tidak sesuai format oleh sistem.
      </p>
    </div>

    <!-- TOMBOL DOWNLOAD -->
    <div
      @click="downloadTemplate"
      class="mt-4 w-full flex flex-col items-center justify-center text-center 
             border-2 border-dashed border-[#0A5C44]/40 rounded-2xl 
             py-8 cursor-pointer hover:border-[#0A5C44] transition-all"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-10 w-10 text-[#0A5C44]/70 mb-2"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
          d="M12 16l4-4m0 0l-4-4m4 4H4m10 4h2a3 3 0 003-3V7a3 3 0 00-3-3h-2" />
      </svg>

      <p class="text-sm font-medium text-[#0A5C44]">
        Klik untuk mendownload template
      </p>
      <p class="text-xs text-gray-400 mt-1">Format: .xlsx</p>
    </div>

  </div>
</template>

<script setup>
import axios from "axios"

// Ambil URL dari .env
const api = import.meta.env.VITE_API_URL

const downloadTemplate = async () => {
  try {
    const res = await axios.get(`${api}/template-excel`, {
      responseType: "blob"
    })

    const blob = new Blob([res.data], {
      type: "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
    })

    const url = window.URL.createObjectURL(blob)
    const a = document.createElement("a")
    a.href = url
    a.download = "Template Data Peserta Panah.xlsx"
    document.body.appendChild(a)
    a.click()
    a.remove()
  } catch (err) {
    console.error(err)
    alert("Gagal mendownload template. Pastikan API URL sudah benar.")
  }
}
</script>

