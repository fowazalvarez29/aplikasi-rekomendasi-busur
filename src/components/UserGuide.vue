<template>
  <div class="space-y-8 bg-white p-6 rounded-2xl border shadow-sm">

    <!-- Judul -->
    <h2 class="text-3xl font-bold text-[#0A5C44]">
      Panduan Pengguna
    <p class="font-thin text-[#0A5C44] text-lg mt-2 text-justify">
      Pengguna aplikasi ini adalah pelatih atau instruktur panahan yang ingin memberikan rekomendasi busur panah yang sesuai untuk murid atau atlet panahan berdasarkan data fisik dan performa mereka.
    </p>
    </h2>

    <!-- Container Steps -->
    <div class="space-y-8">

      <!-- Step 1 -->
      <div class="flex items-start gap-5 bg-[#f8fcfa] border border-[#0A5C44]/20 rounded-2xl p-5 shadow-sm hover:shadow-md transition">
      <div class="w-10 h-10 md:w-12 md:h-12 rounded-full bg-[#0A5C44] text-white flex items-center justify-center text-base md:text-lg font-bold shadow flex-shrink-0">
        1
      </div>
        <div>
          <h3 class="font-semibold text-[#0A5C44] text-lg">
            Input Data Manual
          </h3>
          <p class="text-sm text-gray-700 mt-1 leading-relaxed text-justify">
            1. Klik menu "Input Data".<br>
            2. Isi data siswa satu per satu melalui form input yang disediakan.<br>
            3. Terdapat kolom nama, jenis kelamin, tinggi badan sesuai dengan data siswa.<br>
            4. Masukkan hasil tes fisik push-up dengan ketentuan durasi selama 5 menit.<br>
            5. Masukkan hasil tes fisik sit-up dengan ketentuan durasi selama 5 menit.<br>
            6. Masukkan hasil tes fisik plank dengan ketentuan durasi maksimal 120 detik.<br>
            7. Masukkan hasil tes fisik wall-sit dengan ketentuan durasi maksimal 120 detik.<br>
            8. Pilih tinggi busur yang digunakan dengan pilihan mulai dari 66", 68", dan 70"<br>
            9. Pilih berat busur yang digunakan dengan pilihan mulai dari 16 lbs, 18 lbs, dan 20 lbs.<br>
            10. Isi skor pertemuan latihan dengan ketentuan 5 hingga 12 pertemuan terakhir dan pemberian skor maksimal 180 per sesi.<br>
            11. Setelah semua data terisi, klik tombol "Lihat Rekomendasi" untuk mendapatkan rekomendasi busur panah.
            </p>
        </div>
      </div>

      <!-- Step 2 -->
      <div class="flex items-start gap-5 bg-[#f8fcfa] border border-[#0A5C44]/20 rounded-2xl p-5 shadow-sm hover:shadow-md transition">
         <div class="w-10 h-10 md:w-12 md:h-12 rounded-full bg-[#0A5C44] text-white flex items-center justify-center text-base md:text-lg font-bold shadow flex-shrink-0">
          2
        </div>
        <div>
          <h3 class="font-semibold text-[#0A5C44] text-lg">
            Upload Dokumen Excel
          </h3>
          <p class="text-sm text-gray-700 mt-1 leading-relaxed text-justify">
            1. Klik menu "Upload Dokumen".<br>
            2. Klik bagian kotak yang ada keterangan "Klik untuk memilih file" pada gambar dibawah ini:<br>
            <img :src="tutor1" @click="openImage(tutor1)" class="mt-4 w-full md:w-100 rounded-xl shadow block mx-auto cursor-zoom-in"/><br>
            3. Pilih file dokumen dengan format excel (.xlsx) di folder Anda menyimpan file seperti contoh pada gambar dibawah ini:
            <img :src="tutor2" @click="openImage(tutor2)" class="mt-4 w-100 md:w-30 rounded-xl shadow block mx-auto cursor-zoom-in" /><br>
            4. Klik "Open" atau "Buka"<br>
            5. Tunggu beberapa saat untuk diproses oleh sistem secara otomatis.<br> 
            </p>
        </div>
      </div>

      <!-- Step 3 -->
      <div class="flex items-start gap-5 bg-[#f8fcfa] border border-[#0A5C44]/20 rounded-2xl p-5 shadow-sm hover:shadow-md transition">
         <div class="w-10 h-10 md:w-12 md:h-12 rounded-full bg-[#0A5C44] text-white flex items-center justify-center text-base md:text-lg font-bold shadow flex-shrink-0">
          3
        </div>
        <div>
          <h3 class="font-semibold text-[#0A5C44] text-lg">
            Download Template Dokumen
          </h3>
        <p class="text-sm text-gray-700 mt-1 leading-relaxed text-justify">
            1. Klik menu "Template Dokumen".<br>
            2. Klik bagian kotak yang ada keterangan "Klik untuk mendownload template" pada gambar dibawah ini:<br>
            <img :src="tutor3" @click="openImage(tutor3)" class="mt-4 w-full md:w-100 rounded-xl shadow block mx-auto cursor-zoom-in"/><br>
            3. File template dokumen (.xlsx) akan terdownload secara otomatis.<br>
            4. Isi dari file template dokumen sesuai format yang telah ditentukan agar sistem dapat memproses data dengan benar seperti gambar dibawah ini:<br>
            <img :src="tutor4" @click="openImage(tutor4)" class="mt-4 w-full md:w-100 rounded-xl shadow block mx-auto cursor-zoom-in"/><br>
            5. Pastikan tidak mengubah nama kolom pada template Excel agar file tidak dianggap rusak atau tidak sesuai format oleh sistem.<br>
            6. Untuk penamaan file template dokumen dapat disesuaikan dengan keinginan Anda.<br>
          </p>
        </div>
      </div>
      <!-- Step 4 -->
      <div class="flex items-start gap-5 bg-[#f8fcfa] border border-[#0A5C44]/20 rounded-2xl p-5 shadow-sm hover:shadow-md transition">
         <div class="w-10 h-10 md:w-12 md:h-12 rounded-full bg-[#0A5C44] text-white flex items-center justify-center text-base md:text-lg font-bold shadow flex-shrink-0">
          3
        </div>
        <div>
          <h3 class="font-semibold text-[#0A5C44] text-lg">
            Contoh Isian Data Template
          </h3>
          <p class="text-sm text-gray-700 mt-1 leading-relaxed text-justify">
            1. Klik link berikut untuk melihat file template yang telah terisi data sesuai dengan ketentuan : 
            <a href="https://docs.google.com/spreadsheets/d/1McRabpFTyPTtS_Ie2a5_tG4hgBDBoC8E/edit?usp=sharing&ouid=108347526450048436330&rtpof=true&sd=true" target="_blank" class="text-[#0A5C44] font-semibold hover:underline hover:text-[#094e3b]">
            Data Template
            </a>
          </p>
        </div>
      </div>
    </div>
  </div>
  <!-- Modal Zoom -->
<div
  v-if="showModal"
  class="fixed inset-0 bg-black/70 backdrop-blur-sm flex items-center justify-center z-50 p-4"
>
  <!-- Close Button -->
  <button
    class="absolute top-5 right-5 text-white text-3xl font-bold"
    @click="closeImage"
  >
    ×
  </button>

  <!-- Zoomable Image Container -->
  <div
    class="relative transition duration-300 ease-out"
    :class="zoomAnimation"
    @wheel.prevent="onWheel"
    @mousedown="startDrag"
    @mousemove="onDrag"
    @mouseup="stopDrag"
    @mouseleave="stopDrag"
    @touchstart="startPinch"
    @touchmove="onPinch"
    @touchend="endPinch"
  >
    <img
      :src="modalImage"
      class="rounded-xl shadow-2xl select-none"
      :style="{ transform: 'scale(' + scale + ') translate(' + translateX + 'px,' + translateY + 'px)' }"
    />
  </div>
</div>
</template>

<script setup>
import { ref } from "vue"

// Import gambar
import tutor1 from "@/assets/tutor1.png"
import tutor2 from "@/assets/tutor2.png"
import tutor3 from "@/assets/tutor3.png"
import tutor4 from "@/assets/tutor4.png"

const showModal = ref(false)
const modalImage = ref("")

// Zoom & Pan states
const scale = ref(1)
const translateX = ref(0)
const translateY = ref(0)
const dragging = ref(false)
const startX = ref(0)
const startY = ref(0)

// Animasi
const zoomAnimation = ref("opacity-0 scale-75")

// Pinch variables
let initialDistance = 0
let initialScale = 1

// Open modal
const openImage = (src) => {
  modalImage.value = src
  showModal.value = true
  scale.value = 1
  translateX.value = 0
  translateY.value = 0

  setTimeout(() => {
    zoomAnimation.value = "opacity-100 scale-100"
  }, 20)
}

// Close modal
const closeImage = () => {
  zoomAnimation.value = "opacity-0 scale-75"
  setTimeout(() => {
    showModal.value = false
  }, 200)
}

// Wheel zoom
const onWheel = (e) => {
  const delta = e.deltaY > 0 ? -0.1 : 0.1
  scale.value = Math.min(Math.max(scale.value + delta, 1), 4)
}

// Drag for desktop
const startDrag = (e) => {
  dragging.value = true
  startX.value = e.clientX - translateX.value
  startY.value = e.clientY - translateY.value
}

const onDrag = (e) => {
  if (!dragging.value || scale.value === 1) return
  translateX.value = e.clientX - startX.value
  translateY.value = e.clientY - startY.value
}

const stopDrag = () => {
  dragging.value = false
}

// Pinch-to-zoom for mobile
const startPinch = (e) => {
  if (e.touches.length !== 2) return
  const dx = e.touches[0].clientX - e.touches[1].clientX
  const dy = e.touches[0].clientY - e.touches[1].clientY
  initialDistance = Math.sqrt(dx * dx + dy * dy)
  initialScale = scale.value
}

const onPinch = (e) => {
  if (e.touches.length !== 2) return

  const dx = e.touches[0].clientX - e.touches[1].clientX
  const dy = e.touches[0].clientY - e.touches[1].clientY
  const distance = Math.sqrt(dx * dx + dy * dy)

  const pinchScale = distance / initialDistance
  scale.value = Math.min(Math.max(initialScale * pinchScale, 1), 4)
}

const endPinch = () => {
  initialDistance = 0
}
</script>

