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
        <button @click="deleteEmployee(employee.id)">Hapus</button>
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
    this.fetchEmployees()
  },
  methods: {
    fetchEmployees() {
      axios
        .get('https://abcd1234.ngrok.io/api/employees')
        .then((response) => {
          this.employees = response.data.data
        })
        .catch((error) => {
          console.error('Terjadi kesalahan:', error)
        })
    },
    deleteEmployee(id) {
      axios
        .delete(`https://abcd1234.ngrok.io/api/employees/${id}`)
        .then((response) => {
          console.log('Pegawai berhasil dihapus:', response.data)
          this.fetchEmployees() // Refresh list after deletion
        })
        .catch((error) => {
          console.error('Terjadi kesalahan saat menghapus data:', error)
        })
    }
  }
}
</script>

<style scoped>
/* Tambahkan style CSS jika diperlukan */
</style>
