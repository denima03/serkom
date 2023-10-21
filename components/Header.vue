<template>
    <div class="container">
        <div class="row mt-3 mb-3">
            <div class="col-md-2">
                <img src="/gambar/kota_tasikmalaya.png" class="logo" />
            </div>
            <div class="col-md-10">
                <div class=" mt-3">
                    <h3>
                        <strong>{{ data.nama }} {{ data.judul }}</strong>
                    </h3>
                    <h5>{{ data.sub }}</h5>
                    <p>{{ data.alamat }}</p>
                </div>
            </div>
        </div>
    </div>
</template>


<script setup>
const data = reactive(
    {
        nama: 'WARGA',
        judul: 'RW06 KELURAHAN SUKANAGARA',
        sub: 'Aplikasi Pencarian Data Warga',
        alamat: 'KP.Sukasirna RW06 Kelurahan Sukanagara, Kecamatan Purbaratu Kota Tasikamalaya'
    }
)
</script>

<style scope>
.logo {
    width: 100px
}
</style>