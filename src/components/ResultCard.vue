<template>
<div v-if="data" class="max-w-7xl mx-auto mt-10 bg-white shadow-sm rounded-2xl p-8 border border-gray-100">
    <!-- Header -->
    <div class="bg-[#f3fbf6] border border-[#e6f3eb] rounded-t-2xl px-6 py-4">
      <div class="flex items-center justify-between">
        <h2 class="text-2xl font-semibold text-[#0A5C44] flex items-center gap-3">
          Hasil Rekomendasi
        </h2>
      </div>
    </div>

    <!-- Body -->
    <div class="px-6 py-6">
      <!-- Tombol Export PDF
      <div class="flex justify-end mb-4">
        <button
          @click="exportPDF"
          class="bg-[#0A5C44] hover:bg-[#094e3b] text-white px-6 py-2 rounded-xl text-sm shadow-sm"
        >
          Cetak PDF
        </button>
      </div> -->

      <!-- Top summary -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div>
          <div class="text-xs text-gray-500">Nama Siswa</div>
          <div class="font-semibold text-[#0A5C44] text-lg">{{ data.nama }}</div>
        </div>

        <div>
          <div class="text-xs text-gray-500">Rata-rata Skor per Panah Awal</div>
          <div class="font-semibold text-lg text-[#0A5C44]">{{ data.avgScore }}</div>
        </div>

        <div>
          <div class="text-xs text-gray-500">Data Busur Saat Ini</div>
          <div class="font-semibold text-lg text-[#0A5C44]">
            {{ data.tinggiBusur ? data.tinggiBusur + '"' : '-' }} /
            {{ data.beratBusur ? data.beratBusur + ' lbs' : '-' }}
          </div>
        </div>
      </div>

      <!-- Kategori fisik -->
      <div class="mt-6">
        <h3 class="flex items-center gap-2 text-[#0A5C44] font-semibold">
           Kategori Fisik
        </h3>

        <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mt-4">
          <div
            v-for="(val, i) in data.kategoriFisik"
            :key="i"
            class="space-y-2"
          >
            <div class="text-sm text-gray-600">
              {{ ['Push-Up', 'Sit-Up', 'Plank', 'Wall-Sit'][i] }}
            </div>
            <div class="w-full bg-[#f1f7f2] rounded-full h-8 flex items-center px-3">
              <div
                :class="{
                  'bg-[#2ecc71]': val === 'baik',
                  'bg-[#f1b82d]': val === 'cukup',
                  'bg-[#e74c3c]': val === 'kurang'
                }"
                class="h-6 rounded-full text-white text-xs font-semibold flex items-center justify-center px-3 transition-all duration-300"
                :style="{ width: barWidth(val) }"
              >
                {{ val }}
              </div>
            </div>
          </div>
        </div>

        <!-- Evaluasi -->
        <div class="mt-4 border rounded-lg p-4 bg-white">
          <div class="font-semibold text-gray-700">Evaluasi Fisik Keseluruhan</div>
          <div class="text-sm text-gray-600 mt-2">
            {{ evaluasiText }}
          </div>
        </div>
      </div>

      <!-- Rekomendasi Busur -->
      <div class="mt-6">
        <h3 class="flex items-center gap-2 text-[#0A5C44] font-semibold mb-3">
          Rekomendasi Busur
        </h3>

        <div class="overflow-hidden rounded-lg border">
          <table class="w-full text-sm">
            <thead class="bg-[#edf7f1] text-[#0A5C44]">
              <tr>
                <th class="p-3 text-left font-medium">Tinggi</th>
                <th class="p-3 text-left font-medium">Berat (lbs)</th>
                <th class="p-3 text-left font-medium">Prediksi Skor</th>
                <th class="p-3 text-left font-medium">Presisi</th>
              </tr>
            </thead>
            <tbody class="bg-white">
              <tr
                v-for="rec in data.rekomendasi"
                :key="rec.TinggiBusur + '-' + rec.BeratBusur"
                class="border-t hover:bg-[#f9fdfb]"
              >
                <td class="p-3">{{ rec.TinggiBusur }}"</td>
                <td class="p-3">{{ rec.BeratBusur }} lbs</td>
                <td class="p-3 font-semibold text-[#0A5C44]">{{ rec.Prediksi.toFixed(2) }}</td>
                <td class="p-3">{{ rec.Presisi.toFixed(2) }}%</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Kategori dan Saran -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
        <div class="border rounded-lg p-4 bg-[#fbf6f4]">
          <div class="text-sm text-[#b34f3f]"> Kategori Prediksi Kompetensi Anak</div>
          <div class="mt-2 font-semibold text-lg text-[#6b3d35]">
            {{ data.kategori }}
          </div>
        </div>

        <div class="border rounded-lg p-4 bg-[#f2fbf7]">
          <div class="text-sm text-[#0A5C44] font-semibold">
            Saran Pemilihan Busur
          </div>
          <div class="text-sm text-gray-700 mt-2">
            {{ saranText }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// import pdfMake from "pdfmake/build/pdfmake.min.js"
// import pdfFonts from "pdfmake/build/vfs_fonts.js"
// pdfMake.vfs = pdfFonts.pdfMake.vfs

import pdfMake from "pdfmake/build/pdfmake";
import * as pdfFonts from "pdfmake/build/vfs_fonts";

pdfMake.vfs = pdfFonts.vfs;


import { computed, defineProps } from "vue"

const props = defineProps({
  data: {
    type: Object,
    required: true,
  },
})

// Fungsi lebar bar berdasarkan kategori fisik
const barWidth = (val) => {
  if (val === "baik") return "100%"
  if (val === "cukup") return "70%"
  return "40%"
}

// Evaluasi fisik keseluruhan
const evaluasiText = computed(() => {
  const fisik = props.data.kategoriFisik || []
  const baik = fisik.filter((v) => v === "baik").length
  const kurang = fisik.filter((v) => v === "kurang").length

  if (baik >= 3) return "Sangat Baik — performa fisik optimal."
  if (kurang >= 2) return "Perlu peningkatan fisik."
  return "Cukup baik, pertahankan!"
})

// Saran pemilihan busur sesuai backend
const saranText = computed(() => {
  const kategori = props.data.kategori
  const baik = props.data.kategoriFisik.filter((v) => v === "baik").length

  if (kategori === "High Potential Archer") {
    if (baik >= 3) return "Direkomendasikan memilih berat busur 26–30 lbs."
    if (baik >= 2) return "Direkomendasikan memilih berat busur 22–26 lbs."
    return "Direkomendasikan memilih berat busur 20–22 lbs."
  }

  if (kategori === "Average Archer") {
    if (baik >= 3) return "Direkomendasikan memilih berat busur 22–26 lbs."
    if (baik >= 2) return "Direkomendasikan memilih berat busur 20–24 lbs."
    return "Tingkatkan latihan fisik untuk hasil optimal!"
  }

  return "Tingkatkan latihan dan evaluasi fisik lebih lanjut."
})

const exportPDF = async () => {
  const pdfMake = (await import("pdfmake/build/pdfmake")).default
  const pdfFonts = (await import("pdfmake/build/vfs_fonts")).default
  pdfMake.vfs = pdfFonts.pdfMake.vfs

  const rekomendasiTable = [
    [
      { text: "Tinggi", bold: true, color: "#0A5C44" },
      { text: "Berat", bold: true, color: "#0A5C44" },
      { text: "Prediksi", bold: true, color: "#0A5C44" },
      { text: "Presisi", bold: true, color: "#0A5C44" }
    ],
    ...props.data.rekomendasi.map((r) => [
      r.TinggiBusur + '"',
      r.BeratBusur + " lbs",
      r.Prediksi.toFixed(2),
      r.Presisi.toFixed(2) + "%"
    ])
  ];

  const doc = {
    pageSize: "A4",

    pageMargins: [40, 70, 40, 60],

    header: {
      margin: [40, 15, 40, 0],
      alignment: "center",
      stack: [
        { text: "Laporan Rekomendasi Busur Pemanah", bold: true, fontSize: 20, color: "#0A5C44" },
        { text: "Rekomendasi Busur Pemanah Pemula", fontSize: 10, color: "#555" }
      ]
    },

    footer: (currentPage, pageCount) => ({
      margin: [40, 0, 40, 10],
      fontSize: 8,
      columns: [
        { text: `Halaman ${currentPage} dari ${pageCount}`, alignment: "right", color: "#666" }
      ]
    }),

    content: [
      { text: "DATA SISWA", style: "sectionTitle" },

      {
        table: {
          widths: ["30%", "*"],
          body: [
            ["Nama", props.data.nama],
            ["Rata-Rata Skor Awal", props.data.avgScore],
            ["Busur Saat Ini", `${props.data.tinggiBusur}" / ${props.data.beratBusur} lbs`]
          ]
        },
        layout: "lightHorizontalLines",
        margin: [0, 4, 0, 12]
      },

      { text: "KATEGORI FISIK", style: "sectionTitle" },

      {
        table: {
          widths: ["30%", "*"],
          body: props.data.kategoriFisik.map((v, i) => [
            ["Push-Up", "Sit-Up", "Plank", "Wall-Sit"][i],
            v.toUpperCase()
          ])
        },
        layout: "lightHorizontalLines",
        margin: [0, 4, 0, 10]
      },

      { text: "EVALUASI FISIK", style: "sectionTitle" },
      { text: evaluasiText.value, margin: [0, 0, 0, 12] },

      { text: "REKOMENDASI BUSUR", style: "sectionTitle" },

      {
        table: {
          headerRows: 1,
          widths: ["*", "*", "*", "*"],
          body: rekomendasiTable
        },
        layout: { fillColor: (row) => (row === 0 ? "#e9f7f0" : null) },
        margin: [0, 4, 0, 14]
      },

      { text: "KATEGORI PREDIKSI KOMPETENSI ANAK ", style: "sectionTitle" },
      { text: props.data.kategori, bold: true, color: "#0A5C44", margin: [0, 0, 0, 8] },

      { text: "SARAN PEMILIHAN BUSUR", style: "sectionTitle" },
      { text: saranText.value }
    ],

    styles: {
      sectionTitle: {
        bold: true,
        fontSize: 13,
        color: "#0A5C44",
        margin: [0, 10, 0, 6]
      },
      subheader: {
        bold: true,
        fontSize: 11,
        color: "#0A5C44",
        margin: [0, 8, 0, 4]
      }
    }
  };

  pdfMake.createPdf(doc).download(`Hasil Rekomendasi - ${props.data.nama}.pdf`);
};


</script>


