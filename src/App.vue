<template>
  <div class="container">
    <div class="card">
      <h1>Data Pengguna</h1>
      <p class="description">Tambahkan nama dan alamat pengguna menggunakan form di bawah.</p>

      <form @submit.prevent="addUser">
        <div class="form-group">
          <label for="name">Nama</label>
          <input
            id="name"
            v-model.trim="form.name"
            type="text"
            placeholder="Masukkan nama"
          >
        </div>

        <div class="form-group">
          <label for="address">Alamat</label>
          <textarea
            id="address"
            v-model.trim="form.address"
            placeholder="Masukkan alamat"
          />
        </div>

        <button
          type="submit"
          class="button button-primary"
          :disabled="!isFormValid"
        >
          + Tambah Data
        </button>
      </form>
    </div>

    <div class="card">
      <h2>Daftar Pengguna</h2>

      <div class="counter">Total data: {{ users.length }}</div>

      <div v-if="users.length === 0" class="empty">
        Belum ada data pengguna.
      </div>

      <div
        v-for="(user, index) in users"
        :key="user.id"
        class="user-item"
      >
        <div class="user-info">
          <h3>{{ index + 1 }}. {{ user.name }}</h3>
          <p>{{ user.address }}</p>
        </div>

        <button
          type="button"
          class="button button-danger"
          @click="removeUser(user.id)"
        >
          Hapus
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      form: {
        name: '',
        address: ''
      },
      users: []
    };
  },

  computed: {
    isFormValid() {
      return this.form.name !== '' && this.form.address !== '';
    }
  },

  methods: {
    addUser() {
      if (!this.isFormValid) {
        return;
      }

      this.users.push({
        id: `${Date.now()}-${Math.random().toString(16).slice(2)}`,
        name: this.form.name,
        address: this.form.address
      });

      this.form.name = '';
      this.form.address = '';
    },

    removeUser(id) {
      this.users = this.users.filter((user) => user.id !== id);
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f6f8;
  color: #1f2937;
}

.container {
  max-width: 800px;
  margin: 60px auto;
  padding: 20px;
}

.card {
  background: #fff;
  border-radius: 16px;
  padding: 30px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
  margin-bottom: 20px;
}

h1 {
  margin-top: 0;
  margin-bottom: 8px;
}

.description {
  color: #6b7280;
  margin-bottom: 25px;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
}

input,
textarea {
  width: 100%;
  padding: 12px 14px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 15px;
  outline: none;
  transition: 0.2s;
}

input:focus,
textarea:focus {
  border-color: #6366f1;
  box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

textarea {
  resize: vertical;
  min-height: 100px;
}

.button {
  border: none;
  border-radius: 8px;
  padding: 12px 18px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 600;
}

.button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.button-primary {
  background: #6366f1;
  color: #fff;
}

.button-primary:hover:not(:disabled) {
  background: #4f46e5;
}

.button-danger {
  background: #fee2e2;
  color: #dc2626;
}

.button-danger:hover {
  background: #fecaca;
}

.empty {
  text-align: center;
  padding: 30px;
  color: #9ca3af;
  border: 2px dashed #e5e7eb;
  border-radius: 10px;
}

.user-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  padding: 18px;
  border: 1px solid #e5e7eb;
  border-radius: 10px;
  margin-bottom: 12px;
}

.user-info h3 {
  margin: 0 0 6px;
}

.user-info p {
  margin: 0;
  color: #6b7280;
}

.counter {
  margin-bottom: 15px;
  font-size: 14px;
  color: #6b7280;
}

@media (max-width: 600px) {
  .container {
    margin: 20px auto;
  }

  .user-item {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
