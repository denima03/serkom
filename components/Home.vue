<template>
    <div>
        <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <div class="form-group mb-2">
                        <input v-model="cari" type="search" class="form-control" placeholder="Cari....">
                    </div>
                    <table class="table table-bordered table-striped table-hover">
                        <thead>
                            <tr>
                                <th>NO.</th>
                                <th>NAMA</th>
                                <th>JENIS KELAMIN</th>
                                <th>ALAMAT</th>
                                <th>RT</th>
                                <th>RW</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(warga, i) in cariWarga" :key="warga.id">
                                <td>{{ warga.id }}.</td>
                                <td>{{ warga.nama }}</td>
                                <td>{{ warga.jenis_kelamin }}</td>
                                <td>{{ warga.alamat }}</td>
                                <td>{{ warga.rt }}</td>
                                <td>{{ warga.rw }}</td>
                            </tr>
                        </tbody>
                    </table>
                    <p>{{ cariWarga.length }} item dari {{ total_obj }}</p>
                    <div class="text-center">
                        <button @click='prevPage()' :disabled="prev == ''" class="btn btn-primary me-2">PREV</button>
                        <button @click='nextPage()' :disabled="next == ''" class="btn btn-primary">NEXT</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script setup>
const url = "http://127.0.0.1:8000/api/warga/"
const wargas = ref([])
const cari = ref("")
const total_obj = ref(0)
const total_pages = ref(0)
const next = ref("")
const prev = ref("")

onMounted(() => {
    getData()
})

async function getData() {
    await fetch(url)
        .then(res => res.json())
        .then(data => {
            wargas.value = data.results
            total_obj.value = data.total_objects
            total_pages.value = data.total_pages
            if (data.next) {
                next.value = data.next
            }
            if (data.previous) {
                prev.value = data.previous
            }
        })
}

async function nextPage() {
    await fetch(next.value)
        .then(res => res.json())
        .then(data => {
            wargas.value = data.results
            total_obj.value = data.total_objects
            total_pages.value = data.total_pages
            if (data.next) {
                next.value = data.next
            } else {
                next.value = ''
            }


            if (data.previous) {
                prev.value = data.previous
            } else {
                prev.value = ''
            }
        })
}

async function prevPage() {
    await fetch(prev.value)
        .then(res => res.json())
        .then(data => {
            wargas.value = data.results
            if (data.next) {
                next.value = data.next
            } else {
                next.value = ''
            }

            if (data.previous) {
                prev.value = data.previous
            } else {
                prev.value = ''
            }
        })
}

const cariWarga = computed(() => {
    return wargas.value.filter(b => {
        return (
            b.nama.toLowerCase().includes(cari.value.toLowerCase()) ||
            b.nik.toLowerCase().includes(cari.value.toLowerCase()) ||
            b.alamat.toLowerCase().includes(cari.value.toLowerCase())
        )
    })
})

</script>