<template>
    <q-page padding>
    <q-card flat class="q-gutter-md">
      <q-card-section>
          <div class="text-h5">Input Siswa</div>
          <q-form
               @submit="onSubmit"
               @reset="onReset"
               class="q-mt-lg"
          >
          <div class="q-gutter-md">
              <q-input label="Nama Siswa" v-model="namasiswa" filled :rules="[ val => val && val.length > 0 || 'Tolong isi Nama Siswa']"></q-input>
              <q-input label="Tempat/Tgl/Lahir" v-model="ttl" filled :rules="[ val => val && val.length > 0 || 'Tolong isi ttl']"></q-input>
              <q-input label="NISN" v-model="nisn" filled :rules="[ val => val && val.length > 0 || 'Tolong isi nisn']"></q-input>
              <q-input label="Asal Sekolah" v-model="asalsekolah" filled :rules="[ val => val && val.length > 0 || 'Tolong isi asal sekolah']"></q-input>
              <q-input label="Nama Ortu/Wali" v-model="namaortu" filled :rules="[ val => val && val.length > 0 || 'Tolong isi namaortu']"></q-input>
              <q-input label="Alamat" v-model="alamat" filled :rules="[ val => val && val.length > 0 || 'Tolong isi alamat']"></q-input>
              <q-btn type="submit" label="Input" color="teal" unelevated></q-btn>
              <q-btn type="reset" label="Reset" color="teal" flat unelevated></q-btn>
          </div>
          </q-form>
      </q-card-section>
    </q-card>
    </q-page>
</template>
<script>
export default {
  data () {
    return {
      namasiswa: null,
      ttl: null,
      nisn: null,
      asalsekolah: null,
      namaortu: null,
      alamat: null
    }
  },
  methods: {
    onReset () {
      this.namasiswa = null
      this.ttl = null
      this.nisn = null
      this.asalsekolah = null
      this.namaortu = null
      this.alamat = null
    },
    onSubmit () {
      this.$axios.post('siswa/input', {
        namasiswa: this.namasiswa,
        ttl: this.ttl,
        nisn: this.nisn,
        asalsekolah: this.asalsekolah,
        namaortu: this.namaortu,
        alamat: this.alamat
      }).then(res => {
        if (res.data.sukses) {
          this.$q.notify({
            type: 'positive',
            message: res.data.pesan
          })
          this.$router.push({ name: 'dashboard' })
        } else {
          this.$q.notify({
            type: 'negative',
            message: res.data.pesan
          })
        }
      })
    }
  }
}
</script>
