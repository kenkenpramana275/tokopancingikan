<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import Footer from '../components/Footer.vue';

const router = useRouter();
const categories = ['Semua', 'Joran', 'Reel', 'Umpan', 'Aksesoris'];
const selectedCategory = ref('Semua');

const products = ref([
  {
    id: 1,
    name: "Joran Pancing Premium",
    price: 850000,
    image: "/src/assets/freepik__background__94588.png",
    description: "Joran pancing berkualitas tinggi untuk memancing di laut",
    category: "Joran"
  },
  {
    id: 2,
    name: "Reel Pancing",
    price: 450000,
    image: "/src/assets/freepik__background__91899.png",
    description: "Reel pancing dengan sistem pengereman handal",
    category: "Reel"
  },
  {
    id: 3,
    name: "Set Umpan Pancing",
    price: 125000,
    image: "/src/assets/freepik__background__39182.png",
    description: "Berbagai jenis umpan pancing untuk berbagai jenis ikan",
    category: "Umpan"
  },
  {
    id: 4,
    name: "Senar Pancing Ultra Strong",
    price: 75000,
    image: "/src/assets/image-removebg-preview.png",
    description: "Senar pancing kuat dan tahan lama untuk berbagai kondisi",
    category: "Umpan"
  },
  {
    id: 5,
    name: "Kotak Perlengkapan Pancing",
    price: 195000,
    image: "/src/assets/pngwing.com.png",
    description: "Kotak penyimpanan lengkap untuk semua peralatan pancing",
    category: "Aksesoris"
  },
  {
    id: 6,
    name: "Kursi Lipat Memancing",
    price: 320000,
    image: "/src/assets/pngegg.png",
    description: "Kursi nyaman dan praktis untuk kegiatan memancing",
    category: "Aksesoris"
  },
  {
    id: 7,
    name: "Jaring Pancing Lipat",
    price: 145000,
    image: "/src/assets/pngwing.com_(1).png",
    description: "Jaring pancing praktis untuk menangkap ikan hasil pancingan",
    category: "Aksesoris"
  },
  {
    id: 8,
    name: "Rompi Pancing Multifungsi",
    price: 275000,
    image: "/src/assets/pngwing.com_(2).png",
    description: "Rompi dengan banyak kantong untuk perlengkapan memancing",
    category: "Aksesoris"
  },
  {
    id: 9,
    name: "Topi Pancing Anti UV",
    price: 95000,
    image: "/src/assets/pngwing.com_(3).png",
    description: "Topi perlindungan sinar UV untuk aktivitas memancing",
    category: "Aksesoris"
  }
]);

const filteredProducts = ref([]);

const updateFilteredProducts = () => {
  if (selectedCategory.value === 'Semua') {
    filteredProducts.value = products.value;
  } else {
    filteredProducts.value = products.value.filter(product => product.category === selectedCategory.value);
  }
};

// Initialize filtered products
updateFilteredProducts();

// Watch for category changes
const watchCategory = () => {
  updateFilteredProducts();
};

const formatPrice = (price) => {
  return new Intl.NumberFormat('id-ID', {
    style: 'currency',
    currency: 'IDR'
  }).format(price);
};

const goToProduct = (productId) => {
  router.push(`/products/${productId}`);
};
</script>

<template>

<div class="hero-section">
    <div class="container hero-content">
      <div class="row">
        <div class=" text-white">
          <h1 class="hero-title text-center mb-4">Produk Kami</h1>
          <p class="hero-subtitle text-center mb-4">Silahkan melihat-lihat produk pancing di toko kami.</p>
        </div>
      </div>
    </div>
  </div>
  
  <div class="container py-5 mt-5">
    <h2 class="text-center mb-5">Katalog Produk</h2>
    
    <div class="row mb-4">
      <div class="col-md-12">
        <div class="d-flex justify-content-center gap-2">
          <button
            v-for="category in categories"
            :key="category"
            class="btn"
            :class="selectedCategory === category ? 'btn-primary' : 'btn-outline-primary'"
            @click="selectedCategory = category; watchCategory()"
          >
            {{ category }}
          </button>
        </div>
      </div>
    </div>

    <div class="row g-4">
      <div v-for="product in filteredProducts" :key="product.id" class="col-md-4">
        <div class="card product-card h-100" @click="goToProduct(product.id)" style="cursor: pointer;">
          <img :src="product.image" class="card-img-top" :alt="product.name">
          <div class="card-body">
            <h5 class="card-title">{{ product.name }}</h5>
            <p class="card-text">{{ product.description }}</p>
            <p class="card-text"><strong>{{ formatPrice(product.price) }}</strong></p>
            <button class="btn btn-primary w-100">
              <i class="bi bi-eye me-2"></i>
              Lihat Detail
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <Footer />
</template>

<style scoped>
  .hero-section {
    height: 60vh;
  }
</style>