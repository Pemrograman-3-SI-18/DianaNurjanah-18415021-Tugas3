
<template>
  <q-page>
    <div class="q-pa-md">
      <q-table
        title="Treats"
        :data="data"
        :columns="columns"
        row-key="id"
        :filter="filter"
        :loading="loading"
      >

        <template v-slot:top>
          <q-btn color="teal" :disable="loading" label="Data Transaksi" to="/datatransaksi"/>
          <!--          <q-btn class="q-ml-sm" color="primary" :disable="loading" label="Remove row" @click="removeRow" />-->
          <q-space />
          <q-input borderless dense debounce="300" color="primary" v-model="filter">
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </template>

      </q-table>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      filter: '',
      rowCount: 10,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Kode Transaksi',
          align: 'left',
          field: row => row.kodetransaksi,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'namapembeli', align: 'center', label: 'Nama Pembeli', field: 'namapembeli', sortable: true },
        { name: 'judulbuku', align: 'center', label: 'Judul Buku', field: 'judulbuku', sortable: true },
        { name: 'hargabuku', label: 'Harga Buku', align: 'center', field: 'hargabuku' },
        { name: 'jumlahbuku', label: 'Jumlah Buku', align: 'center', field: 'jumlahbuku' },
        { name: 'total', label: 'Total', align: 'center', field: 'total' }

      ],
      data: [
        {
          kodetransaksi: 'Trasn-001',
          namapembeli: 'John Petrucci',
          judulbuku: 'Pemograman 3',
          hargabuku: '250000',
          jumlahbuku: '2',
          total: '500000'

        },
        {
          kodetransaksi: 'Trasn-002',
          namapembeli: 'Yngwie Malmsteen',
          judulbuku: 'Pemograman 3',
          hargabuku: '250000',
          jumlahbuku: '1',
          total: '250000'
        },
        {
          kodetransaksi: 'Trasn-003',
          namapembeli: 'Slash',
          judulbuku: 'Prak Pemograman 3',
          hargabuku: '350000',
          jumlahbuku: '3',
          total: '1050000'

        }

      ]
    }
  },

  methods: {
    // emulate fetching data from server
    addRow () {
      this.loading = true
      setTimeout(() => {
        const
          index = Math.floor(Math.random() * (this.data.length + 1)),
          row = this.original[Math.floor(Math.random() * this.original.length)]
        if (this.data.length === 0) {
          this.rowCount = 0
        }
        row.id = ++this.rowCount
        const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
        this.data = [...this.data.slice(0, index), addRow, ...this.data.slice(index)]
        this.loading = false
      }, 500)
    },

    removeRow () {
      this.loading = true
      setTimeout(() => {
        const index = Math.floor(Math.random() * this.data.length)
        this.data = [...this.data.slice(0, index), ...this.data.slice(index + 1)]
        this.loading = false
      }, 500)
    }
  }
}
</script>
