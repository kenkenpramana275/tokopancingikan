<script setup>
import { ref, computed } from 'vue';
import { useRouter, useRoute } from 'vue-router';

const router = useRouter();
const route = useRoute();
const cartCount = ref(0);
const isScrolled = ref(false);

const isCartPage = computed(() => {
  return route.path === '/cart';
});

if (typeof window !== 'undefined') {
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 50;
  });
}
</script>

<template>
  <nav class="navbar navbar-expand-lg" :class="[
    isCartPage 
      ? 'bg-primary navbar-dark' 
      : [isScrolled ? 'navbar-scrolled navbar-light' : 'navbar-transparent navbar-dark']
  ]">
    <div class="container">
      <router-link class="navbar-brand" to="/">
        <i class="bi bi-water me-2"></i>
        Toko Pancing
      </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav me-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Beranda</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/products">Produk</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">Tentang Kami</router-link>
          </li>
        </ul>
        <div class="d-flex">
          <router-link 
            to="/cart"
            class="btn position-relative"
            :class="isCartPage ? 'btn-light' : [isScrolled ? 'btn-primary' : 'btn-outline-light']"
          >
            <i class="bi bi-cart"></i> Keranjang
            <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger cart-badge">
              {{ cartCount }}
            </span>
          </router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  transition: all 0.3s ease-in-out;
  padding: 10px 0;
}

.bg-primary {
  background-color: #0d6efd !important;
}

.navbar-scrolled {
  background-color: rgba(255, 255, 255, 0.95);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.navbar-transparent {
  background-color: transparent;
}

.cart-badge {
  transform: translate(50%, -50%) !important;
}
</style>