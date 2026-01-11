<template>
  <div class="bg-white p-6 rounded-2xl border shadow-sm">

    <label class="font-medium text-[#0A5C44] text-xl">Upload Dokumen (Excel)</label>
    <p class="text-xs text-gray-500 mt-1">
      Silakan unggah file Excel (.xlsx) yang berisi data untuk diproses secara otomatis.
    </p>

    <label
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
          d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1M16 12l-4-4m0 0l-4 4m4-4v12" />
      </svg>

      <p class="text-sm font-medium text-[#0A5C44]">Klik untuk memilih file</p>
      <p class="text-xs text-gray-400 mt-1">Format yang diizinkan: .xlsx</p>

      <input
        type="file"
        accept=".xlsx"
        @change="uploadExcel"
        class="hidden"
      />
    </label>

  </div>
</template>



<script setup>
import axios from "axios"
const emit = defineEmits(["hasilExcel"])

// Base URL dari .env
const api = import.meta.env.VITE_API_URL

const uploadExcel = async (e) => {
  const file = e.target.files[0]
  if (!file) return

  const formData = new FormData()
  formData.append("file", file)

  try {
    const res = await axios.post(
      `${api}/predict-excel`,  // 🔥 SUDAH BENAR
      formData,
      {
        headers: { "Content-Type": "multipart/form-data" },
      }
    )

    emit("hasilExcel", res.data)

  } catch (err) {
    console.error(err)
    alert("Gagal memproses Excel! Periksa kembali file atau server API.")
  }
}
</script>

