<template>
  <div>
    <h1>Daftar Pegawai</h1>
    <ul>
      <li v-for="employee in employees" :key="employee.id">
        <h3>{{ employee.nama_pegawai }}</h3>
        <p>NIK: {{ employee.nik }}</p>
        <p>Jabatan: {{ employee.id_jabatan }}</p>
        <p>Mulai Cuti: {{ employee.mulai_cuti }}</p>
        <p>Akhir Cuti: {{ employee.akhir_cuti }}</p>
        <p>Jenis Cuti: {{ employee.id_jenis_cuti }}</p>
        <p>Jumlah Cuti: {{ employee.jumlah_cuti }}</p>
        <p>Sisa Cuti: {{ employee.sisa_cuti }}</p>
        <p>Keterangan: {{ employee.keterangan }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      employees: []
    }
  },
  mounted() {
    axios
      .get('http://127.0.0.1:8000/api/leave')
      .then((response) => {
        this.employees = response.data.data
        console.log(response.data.data)
      })
      .catch((error) => {
        console.error('Terjadi kesalahan:', error)
      })
  }
}
</script>
