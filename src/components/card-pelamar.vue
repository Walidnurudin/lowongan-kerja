<template>
  <v-card class="mx-auto" max-width="400">
    <v-img class="white--text align-end" height="200px" :src="foto">
      <v-card-title class="text--primary">{{nama}}</v-card-title>
    </v-img>

    <v-card-text class="text--primary">
      <h1>{{lowongan}}</h1>

      <div>{{alamat}}</div>
    </v-card-text>

    <v-card-actions>
      <modalPelamar v-show="lamar" />
      <router-link class="text-decoration-none" :to="`/pelamar/perusahaan/${route}`" v-show="btnDetail">
        <v-btn color="primary" class="ml-2" outlined text>Detail</v-btn>
      </router-link>
      <v-btn color="error" class="ml-2" @click="del()" v-show="btnDel" text>Hapus</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import modalPelamar from "./modal-pelamar.vue";
import vue from "@/assets/logo.png";

export default {
  data: () => {
    return {
      foto: vue
    };
  },
  components: {
    modalPelamar
  },
  props: [
    "nama",
    "alamat",
    "deskripsi",
    "lowongan",
    "btnDel",
    "id",
    'route',
    "btnDetail",
    "lamar"
  ],
  methods: {
    del: function() {
      this.$swal({
        title: "Hapus lowongan ini?",
        confirmButtonText: "Hapus",
        cancelButtonText: "Tidak",
        showCancelButton: true
      }).then(result => {
        if (result.isConfirmed) {
          this.$swal("Terhapus", "", "success");
          this.$store.dispatch("hapusPerusahaan", this.id);
        }
      });
    }
  }
};
</script>