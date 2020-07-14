<template>
  <q-page padding>
<q-table
      title="Nama Siswa"
      :data="data"
      :columns="columns"
      row-key="name"
    >
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="namasiswa" :props="props">
            {{ props.row.namasiswa }}
          </q-td>
          <q-td key="ttl" :props="props">
            {{ props.row.ttl }}
          </q-td>
          <q-td key="nisn" :props="props">
            {{ props.row.nisn }}
          </q-td>
           <q-td key="asalsekolah" :props="props">
            {{ props.row.asalsekolah }}
          </q-td>
           <q-td key="namaortu" :props="props">
            {{ props.row.namaortu }}
          </q-td>
          <q-td key="alamat" :props="props">
            {{ props.row.alamat }}
          </q-td>
          <q-td key="aksi" :props="props">
            <div class="row">
              <div class="col">
                <q-btn label="Edit" :to="{ name: 'formEditSiswa', params: { id: props.row._id}}" color="orange" icon="edit" unelevated></q-btn>
               </div>
              <div class="col">
                <q-btn label="Hapus" @click="confirm(props.row._id)" color="negative" icon="delete" unelevated></q-btn>
               </div>
              </div>
          </q-td>
        </q-tr>
      </template>
    </q-table>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      columns: [
        { name: 'namasiswa', align: 'center', label: 'Nama Siswa', field: 'namasiswa', sortable: true },
        { name: 'ttl', label: 'Tempat/Tgl/Lahir', align: 'center', field: 'ttl', sortable: true },
        { name: 'nisn', label: 'NISN', align: 'center', field: 'nisn', sortable: true },
        { name: 'asalsekolah', label: 'Asal Sekolah', align: 'center', field: 'asalsekolah', sortable: true },
        { name: 'namaortu', label: 'Nama OrangTua', align: 'center', field: 'namaorangtua', sortable: true },
        { name: 'alamat', label: 'Alamat', align: 'center', field: 'alamat', sortable: true },
        { name: 'aksi', label: 'Aksi', field: 'aksi', align: 'center' }
      ],
      data: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('siswa/tampil')
        .then(res => {
          if (res.data.sukses) {
            this.data = res.data.data
          } else {
            this.$q.notify({
              type: 'negative',
              message: res.data.pesan
            })
          }
        })
    },
    confirm (id) {
      this.$q.dialog({
        title: 'Konfirmasi',
        message: 'Apakah Anda Yakin Menghapus Data Siswa Ini ?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.$axios.delete('siswa/delete/' + id)
          .then((res) => {
            if (res.data.sukses) {
              this.$q.notify({
                type: 'positive',
                message: res.data.pesan
              })
              this.getData()
            } else {
              this.$q.notify({
                type: 'negative',
                message: res.data.pesan
              })
            }
          })
      })
    }
  }
}
</script>
