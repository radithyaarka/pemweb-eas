<template>
    <div class="max-w-md mx-auto mt-8 p-6 bg-gray-100 rounded-md shadow-md">
      <h2 class="text-2xl mb-4 font-semibold">Form Registrasi Lomba</h2>
      <form @submit.prevent="submitForm">
        <div class="mb-4">
          <label for="nama" class="block text-sm font-medium text-gray-600">Nama:</label>
          <input type="text" id="nama" v-model="formData.nama" required class="mt-1 p-2 border border-gray-300 rounded-md w-full focus:outline-none focus:border-blue-500" />
        </div>
        <div class="mb-4">
          <label for="email" class="block text-sm font-medium text-gray-600">Email:</label>
          <input type="email" id="email" v-model="formData.email" required class="mt-1 p-2 border border-gray-300 rounded-md w-full focus:outline-none focus:border-blue-500" />
        </div>
        <div class="mb-4">
          <label for="asal_sekolah" class="block text-sm font-medium text-gray-600">Asal Sekolah:</label>
          <input type="text" id="asal_sekolah" v-model="formData.asal_sekolah" required class="mt-1 p-2 border border-gray-300 rounded-md w-full focus:outline-none focus:border-blue-500" />
        </div>
        <div class="mb-4">
          <label for="tanggal_pendaftaran" class="block text-sm font-medium text-gray-600">Tanggal Pendaftaran:</label>
          <input type="date" id="tanggal_pendaftaran" v-model="formData.tanggal_pendaftaran" required class="mt-1 p-2 border border-gray-300 rounded-md w-full focus:outline-none focus:border-blue-500" />
        </div>
        <button type="submit" class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-600 focus:outline-none focus:shadow-outline-blue active:bg-blue-800">
          Daftar
        </button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          nama: '',
          email: '',
          asal_sekolah: '',
          tanggal_pendaftaran: '',
        },
      };
    },
    methods: {
      async submitForm() {
        try {
          const apiUrl = 'http://localhost:3100/api/pendaftaran';
  
          const response = await fetch(apiUrl, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify(this.formData),
          });
  
          const responseData = await response.json();
  
          console.log('Data Pendaftaran Berhasil Dikirim:', responseData);
  
          // Reset form setelah pengiriman
          this.formData = {
            nama: '',
            email: '',
            asal_sekolah: '',
            tanggal_pendaftaran: '',
          };
        } catch (error) {
          console.error('Terjadi kesalahan saat mengirim data:', error);
        }
      },
    },
  };
  </script>
  