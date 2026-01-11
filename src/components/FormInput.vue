<template>
  <div class="max-w-7xl mx-auto bg-white shadow-sm rounded-2xl p-8 mt-10 border border-gray-100">
    <h3 class="text-xl font-semibold text-[#0A5C44] flex items-center mb-2">Data Siswa</h3>
    <p class="text-sm text-gray-500 mb-6">
      Lengkapi formulir berikut untuk mendapatkan rekomendasi busur yang sesuai.
    </p>

    <form @submit.prevent="handleSubmit" class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <!-- Nama -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Nama Siswa</label>

        <input
          v-model.trim="form.nama"
          @input="onNamaInput"
          type="text"
          required
          placeholder="Masukkan nama lengkap"
          :aria-invalid="errors.nama ? 'true' : 'false'"
          :class="inputClass(errors.nama, shake.nama)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        />

        <p v-if="errors.nama" class="text-xs text-red-600 mt-1">
          Nama hanya boleh berisi huruf dan spasi.
        </p>
      </div>

      <!-- Jenis Kelamin -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Jenis Kelamin</label>

        <div
          class="flex items-center gap-4 mt-2 rounded-xl p-2.5 border"
          :class="
            (errors.gender ? 'border-red-500 bg-red-50' : 'border-gray-200') +
            (shake.gender ? ' shake' : '')
          "
        >
          <label class="flex items-center text-sm text-gray-700">
            <input
              type="radio"
              v-model="form.gender"
              value="L"
              class="mr-2 accent-[#0A5C44]"
              @change="validateGender"
            />
            Laki-laki
          </label>
          <label class="flex items-center text-sm text-gray-700">
            <input
              type="radio"
              v-model="form.gender"
              value="P"
              class="mr-2 accent-[#0A5C44]"
              @change="validateGender"
            />
            Perempuan
          </label>
        </div>

        <p v-if="errors.gender" class="text-xs text-red-600 mt-1">Jenis kelamin wajib dipilih.</p>
      </div>

      <!-- Tinggi Badan -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Tinggi Badan (cm)</label>

        <input
          :value="displayNumber(form.tinggi)"
          @input="onNumberInput('tinggi', $event, 100, 200)"
          type="text"
          inputmode="numeric"
          pattern="^[0-9]+$"
          minlength="3"
          maxlength="3"
          required
          placeholder="Contoh: 165"
          :aria-invalid="errors.tinggi ? 'true' : 'false'"
          :class="inputClass(errors.tinggi, shake.tinggi)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        />

        <p v-if="errors.tinggi" class="text-xs text-red-600 mt-1">Tinggi badan harus 100–200 cm.</p>
      </div>

      <!-- Push-Up -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Push-Up (5 menit)</label>

        <input
          :value="displayNumber(form.pushUp)"
          @input="onNumberInput('pushUp', $event, 0, 50)"
          type="text"
          inputmode="numeric"
          pattern="^[0-9]+$"
          required
          placeholder="Jumlah push-up"
          :aria-invalid="errors.pushUp ? 'true' : 'false'"
          :class="inputClass(errors.pushUp, shake.pushUp)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        />

        <p v-if="errors.pushUp" class="text-xs text-red-600 mt-1">Push-up harus 0–50.</p>
      </div>

      <!-- Sit-Up -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Sit-Up (5 menit)</label>

        <input
          :value="displayNumber(form.sitUp)"
          @input="onNumberInput('sitUp', $event, 0, 50)"
          type="text"
          inputmode="numeric"
          pattern="^[0-9]+$"
          required
          placeholder="Jumlah sit-up"
          :aria-invalid="errors.sitUp ? 'true' : 'false'"
          :class="inputClass(errors.sitUp, shake.sitUp)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        />

        <p v-if="errors.sitUp" class="text-xs text-red-600 mt-1">Sit-up harus 0–50.</p>
      </div>

      <!-- Plank -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Plank (detik, maks. 120)</label>

        <input
          :value="displayNumber(form.plank)"
          @input="onNumberInput('plank', $event, 0, 120)"
          type="text"
          inputmode="numeric"
          pattern="^[0-9]+$"
          required
          placeholder="Durasi plank"
          :aria-invalid="errors.plank ? 'true' : 'false'"
          :class="inputClass(errors.plank, shake.plank)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        />

        <p v-if="errors.plank" class="text-xs text-red-600 mt-1">Plank harus 0–120 detik.</p>
      </div>

      <!-- Wall-Sit -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Wall-Sit (detik, maks. 120)</label>

        <input
          :value="displayNumber(form.wallSit)"
          @input="onNumberInput('wallSit', $event, 0, 120)"
          type="text"
          inputmode="numeric"
          pattern="^[0-9]+$"
          required
          placeholder="Durasi wall-sit"
          :aria-invalid="errors.wallSit ? 'true' : 'false'"
          :class="inputClass(errors.wallSit, shake.wallSit)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        />

        <p v-if="errors.wallSit" class="text-xs text-red-600 mt-1">Wall-sit harus 0–120 detik.</p>
      </div>

      <!-- Tinggi Busur -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Tinggi Busur yang Dipakai</label>

        <select
          v-model.number="form.tinggiBusur"
          @change="validateSelect('tinggiBusur')"
          required
          :aria-invalid="errors.tinggiBusur ? 'true' : 'false'"
          :class="selectClass(errors.tinggiBusur, shake.tinggiBusur)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        >
          <option disabled :value="null">Pilih tinggi busur</option>
          <option :value="66">66"</option>
          <option :value="68">68"</option>
          <option :value="70">70"</option>
        </select>

        <p v-if="errors.tinggiBusur" class="text-xs text-red-600 mt-1">
          Tinggi busur wajib dipilih.
        </p>
      </div>

      <!-- Berat Busur -->
      <div>
        <label class="font-medium text-[#0A5C44] text-sm">Berat Busur yang Dipakai</label>

        <select
          v-model.number="form.beratBusur"
          @change="validateSelect('beratBusur')"
          required
          :aria-invalid="errors.beratBusur ? 'true' : 'false'"
          :class="selectClass(errors.beratBusur, shake.beratBusur)"
          class="w-full mt-1 rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
        >
          <option disabled :value="null">Pilih berat busur</option>
          <option :value="16">16 lbs</option>
          <option :value="18">18 lbs</option>
          <option :value="20">20 lbs</option>
        </select>

        <p v-if="errors.beratBusur" class="text-xs text-red-600 mt-1">Berat busur wajib dipilih.</p>
      </div>

      <!-- Skor Pertemuan -->
      <div class="md:col-span-2">
        <div class="mt-4 border-t pt-4">
          <h3 class="text-sm font-semibold text-[#0A5C44] flex items-center mb-2">
            Skor Pertemuan Latihan
          </h3>
          <p class="text-xs text-gray-500 mb-3">
            Isi minimal 5 skor pertemuan (maksimal 12 pertemuan). Skor per sesi 0–180.
          </p>

          <div
            v-for="(score, index) in form.scores"
            :key="index"
            class="flex items-start gap-2 mb-2"
          >
            <div class="w-full">
              <input
                :value="displayNumber(form.scores[index])"
                @input="onScoreInput(index, $event)"
                type="text"
                inputmode="numeric"
                pattern="^[0-9]+$"
                placeholder="Skor pertemuan"
                :aria-invalid="errors.scores[index] ? 'true' : 'false'"
                :class="inputClass(errors.scores[index], shake.scores[index])"
                class="w-full rounded-xl p-2.5 text-sm focus:ring-2 focus:ring-[#0A5C44] focus:outline-none border"
              />
              <p v-if="errors.scores[index]" class="text-xs text-red-600 mt-1">Skor harus 0–180.</p>
            </div>

            <span class="text-xs text-gray-400 pt-3">/180</span>
          </div>

          <p v-if="errors.scoresMin" class="text-xs text-red-600 mt-2">
            Minimal isi 5 skor pertemuan yang valid.
          </p>
        </div>
      </div>

      <!-- Tombol -->
      <div class="md:col-span-2 mt-6 text-center">
        <button
          type="submit"
          class="bg-[#0A5C44] hover:bg-[#094e3b] text-white px-8 py-2.5 rounded-xl font-medium text-sm transition-all shadow-sm disabled:opacity-60 disabled:cursor-not-allowed"
          :disabled="isSubmitting"
        >
          {{ isSubmitting ? 'Memproses...' : 'Lihat Rekomendasi' }}
        </button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'
import axios from 'axios'

const emit = defineEmits(['hasilManual'])
const isSubmitting = ref(false)

const form = reactive({
  nama: '',
  gender: '',
  tinggi: null,
  pushUp: null,
  sitUp: null,
  plank: null,
  wallSit: null,
  tinggiBusur: null,
  beratBusur: null,
  scores: [null],
})

const errors = reactive({
  nama: false,
  gender: false,
  tinggi: false,
  pushUp: false,
  sitUp: false,
  plank: false,
  wallSit: false,
  tinggiBusur: false,
  beratBusur: false,
  scores: [],
  scoresMin: false,
})

const shake = reactive({
  nama: false,
  gender: false,
  tinggi: false,
  pushUp: false,
  sitUp: false,
  plank: false,
  wallSit: false,
  tinggiBusur: false,
  beratBusur: false,
  scores: [],
})

const inputClass = (isError, isShake) => {
  return [isError ? 'border-red-500 bg-red-50' : 'border-gray-200', isShake ? 'shake' : ''].join(
    ' ',
  )
}

const selectClass = (isError, isShake) => {
  return [isError ? 'border-red-500 bg-red-50' : 'border-gray-200', isShake ? 'shake' : ''].join(
    ' ',
  )
}

// ---------- Helpers ----------
const displayNumber = (v) => (v === null || v === undefined ? '' : String(v))

const onlyDigits = (raw) => String(raw ?? '').replace(/\D/g, '')

const toNumberOrNull = (digits) => {
  if (digits === '') return null
  const n = Number(digits)
  return Number.isNaN(n) ? null : n
}

const validateRange = (val, min, max) => {
  if (val === null) return true // kosong dianggap error kalau required
  return val < min || val > max
}

const triggerShake = (field) => {
  // field bisa string atau { type:'scores', index:n }
  if (typeof field === 'string') {
    shake[field] = true
    setTimeout(() => (shake[field] = false), 450)
    return
  }
  if (field?.type === 'scores') {
    shake.scores[field.index] = true
    setTimeout(() => (shake.scores[field.index] = false), 450)
  }
}

// ---------- Validasi Nama ----------
const namaRegex = /^[A-Za-zÀ-ÿ\s]+$/

const onNamaInput = (e) => {
  // Filter langsung: hapus selain huruf dan spasi
  form.nama = form.nama.replace(/[^A-Za-zÀ-ÿ\s]/g, '')
  // Validasi
  errors.nama = form.nama.trim() === '' || !namaRegex.test(form.nama)
}

const validateGender = () => {
  errors.gender = !form.gender
}

const validateSelect = (key) => {
  errors[key] = form[key] === null || form[key] === undefined || form[key] === ''
}

// ---------- Input Angka (umum) ----------
const onNumberInput = (key, event, min, max) => {
  const digits = onlyDigits(event.target.value)
  const num = toNumberOrNull(digits)
  form[key] = num

  // set balik ke input agar karakter non-digit hilang di UI
  event.target.value = digits

  errors[key] = validateRange(num, min, max)
}

// ---------- Skor ----------
const onScoreInput = (index, event) => {
  const digits = onlyDigits(event.target.value)
  const num = toNumberOrNull(digits)
  form.scores[index] = num
  event.target.value = digits

  // validasi 0–180
  errors.scores[index] = validateRange(num, 0, 180)

  // tambahkan input baru jika:
  // - input terakhir terisi
  // - nilainya valid
  // - belum sampai 12
  const isLast = index === form.scores.length - 1
  const isFilled = num !== null
  const isValid = !errors.scores[index]

  if (isLast && isFilled && isValid && form.scores.length < 12) {
    form.scores.push(null)
    errors.scores.push(false)
    shake.scores.push(false)
  }
}

// ---------- Validasi Final ----------
const validateAll = () => {
  // nama
  errors.nama = form.nama.trim() === '' || !namaRegex.test(form.nama)

  // gender
  errors.gender = !form.gender

  // angka required + range
  errors.tinggi = validateRange(form.tinggi, 100, 220)
  errors.pushUp = validateRange(form.pushUp, 0, 500)
  errors.sitUp = validateRange(form.sitUp, 0, 500)
  errors.plank = validateRange(form.plank, 0, 120)
  errors.wallSit = validateRange(form.wallSit, 0, 120)

  // select
  errors.tinggiBusur = form.tinggiBusur === null
  errors.beratBusur = form.beratBusur === null

  // scores: hitung yang valid & terisi
  const filledValidScores = form.scores
    .map((v, i) => {
      errors.scores[i] = validateRange(v, 0, 180) && v !== null
      return { v, i }
    })
    .filter((x) => x.v !== null && !validateRange(x.v, 0, 180))
    .map((x) => Number(x.v))

  errors.scoresMin = filledValidScores.length < 5

  // daftar field error untuk shake
  const fieldsToShake = []
  if (errors.nama) fieldsToShake.push('nama')
  if (errors.gender) fieldsToShake.push('gender')
  if (errors.tinggi) fieldsToShake.push('tinggi')
  if (errors.pushUp) fieldsToShake.push('pushUp')
  if (errors.sitUp) fieldsToShake.push('sitUp')
  if (errors.plank) fieldsToShake.push('plank')
  if (errors.wallSit) fieldsToShake.push('wallSit')
  if (errors.tinggiBusur) fieldsToShake.push('tinggiBusur')
  if (errors.beratBusur) fieldsToShake.push('beratBusur')

  // shake score yang error dan terisi / atau kosong tapi dibutuhkan minimal
  form.scores.forEach((v, i) => {
    const isWrong = v !== null && validateRange(v, 0, 180)
    if (isWrong) fieldsToShake.push({ type: 'scores', index: i })
  })

  return { filledValidScores, fieldsToShake }
}

const hasAnyError = () => {
  if (
    errors.nama ||
    errors.gender ||
    errors.tinggi ||
    errors.pushUp ||
    errors.sitUp ||
    errors.plank ||
    errors.wallSit ||
    errors.tinggiBusur ||
    errors.beratBusur ||
    errors.scoresMin
  )
    return true

  // score error yang terisi
  for (let i = 0; i < (errors.scores?.length || 0); i++) {
    if (errors.scores[i]) return true
  }
  return false
}

// ---------- Submit ----------
const handleSubmit = async () => {
  const { filledValidScores, fieldsToShake } = validateAll()

  if (hasAnyError()) {
    // shake field yang error
    fieldsToShake.forEach((f) => {
      if (typeof f === 'string') triggerShake(f)
      else triggerShake(f)
    })

    // shake juga indikator skor minimal bila kurang
    if (errors.scoresMin) {
      // shake 5 input pertama sebagai hint (jika ada)
      for (let i = 0; i < Math.min(5, form.scores.length); i++) {
        triggerShake({ type: 'scores', index: i })
      }
    }

    alert('Masih ada input yang tidak sesuai atau belum terisi.')
    return
  }

  isSubmitting.value = true
  try {
    const payload = {
      nama: form.nama,
      gender: form.gender,
      tinggi: Number(form.tinggi),
      pushUp: Number(form.pushUp),
      sitUp: Number(form.sitUp),
      plank: Number(form.plank),
      wallSit: Number(form.wallSit),
      tinggiBusur: Number(form.tinggiBusur),
      beratBusur: Number(form.beratBusur),
      scores: filledValidScores,
    }

    const res = await axios.post('http://127.0.0.1:5000/predict', payload)
    emit('hasilManual', res.data)
  } catch (err) {
    console.error('Gagal mengambil data dari backend:', err)
    alert('Terjadi kesalahan saat mengambil rekomendasi dari server.')
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  15% {
    transform: translateX(-6px);
  }
  30% {
    transform: translateX(6px);
  }
  45% {
    transform: translateX(-5px);
  }
  60% {
    transform: translateX(5px);
  }
  75% {
    transform: translateX(-3px);
  }
  90% {
    transform: translateX(3px);
  }
}
.shake {
  animation: shake 0.45s ease-in-out;
}
</style>
