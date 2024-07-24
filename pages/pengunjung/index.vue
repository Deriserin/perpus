<template>
< class="container">
    <div class="row">
        <div class="col-lg-12">
            <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
            <div class="my-3">
                <input type="search" class="form-control form-control-lg rounded-5" placeholder="Filter..."/>                    
            </div>
            <div class="my-3 text-muted">MENAMPILKAN RIWAYAT KUNJUNGAN</div>
            <table class="table">
                <thead>
                    <tr>
                        <td>#</td>
                        <td>NAMA</td>
                        <td>KEANGGOTAAN</td>
                        <td>WAKTU</td>
                        <td>KEPERLUAN</td>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(visitor, i) in visitors" :key="i">
                        <td>{{ i + 1.}}</td>
                        <td>{{ visitor.nama }}</td>
                        <td>{{ visitor.keaaggotaan.nama }}</td>
                        <td>{{ visitor.tanggal }}</td>
                        <td>{{ visitor.keperluan.nama }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
        <<nuxt-link to="pengunjung/tambah">
        <button type="button" class="btn btn-dark bck mt-4">kembali</button>
    </nuxt-link>
</template>

<script setup>
const uspabase = useSupabaseClient()

const visitors = ref ([]);

const getpengunjung = async () => {
    const { data, error } = await supabase.from("pengunjung").select(`*, keanggotaan(*), keperluan(*)`);
    if (data) visitors.value = data;
};
onMounted(() => {
getpengunjung();
})
</script>