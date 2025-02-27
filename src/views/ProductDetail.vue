<script setup>
import { ref, onMounted, computed } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

const isProductDetailPage = computed(() => {
  return route.path.includes('/products/');
});

const product = ref(null);
const cartCount = ref(0);

const products = [
  {
    id: 1,
    name: "Joran Pancing Premium",
    price: 850000,
    image: "/src/assets/freepik__background__94588.png",
    description: "Joran pancing berkualitas tinggi untuk memancing di laut",
    longDescription: "Joran pancing premium dengan panjang 2.7 meter, terbuat dari bahan carbon fiber berkualitas tinggi. Cocok untuk memancing di laut dan danau. Dilengkapi dengan ring guide stainless steel dan handle EVA yang nyaman.",
    specifications: [
      "Panjang: 2.7 meter",
      "Material: Carbon Fiber",
      "Berat: 280 gram",
      "Ring Guide: Stainless Steel",
      "Handle: EVA Foam"
    ]
  },
  {
    id: 2,
    name: "Reel Pancing",
    price: 450000,
    image: "/src/assets/freepik__background__91899.png",
    description: "Reel pancing dengan sistem pengereman handal",
    longDescription: "Reel pancing berkualitas dengan sistem pengereman yang handal dan smooth. Dilengkapi dengan 8 ball bearing dan gear ratio 5.2:1 untuk pengalaman memancing yang optimal.",
    specifications: [
      "Ball Bearings: 8",
      "Gear Ratio: 5.2:1",
      "Berat: 230 gram",
      "Line Capacity: 0.285mm/245m",
      "Max Drag: 7kg"
    ]
  },
  {
    id: 3,
    name: "Set Umpan Pancing",
    price: 125000,
    image: "/src/assets/freepik__background__39182.png",
    description: "Berbagai jenis umpan pancing untuk berbagai jenis ikan",
    longDescription: "Set lengkap umpan pancing yang terdiri dari berbagai jenis umpan buatan. Cocok untuk memancing berbagai jenis ikan air tawar maupun air laut. Dilengkapi dengan box penyimpanan yang praktis.",
    specifications: [
      "Jumlah Umpan: 20 pcs",
      "Jenis: Soft bait & Hard bait",
      "Ukuran: 5-10 cm",
      "Warna: Bervariasi",
      "Material: Plastik & Karet Khusus"
    ]
  },
  {
    id: 4,
    name: "Senar Pancing Ultra Strong",
    price: 75000,
    image: "/src/assets/image-removebg-preview.png",
    description: "Senar pancing kuat dan tahan lama untuk berbagai kondisi",
    longDescription: "Senar pancing berkualitas tinggi dengan kekuatan tarik yang luar biasa. Terbuat dari bahan fluorocarbon yang tahan terhadap abrasi dan hampir tidak terlihat di dalam air. Ideal untuk memancing di berbagai kondisi perairan.",
    specifications: [
      "Panjang: 100 meter",
      "Material: Fluorocarbon",
      "Kekuatan Tarik: 15 kg",
      "Diameter: 0.35 mm",
      "Warna: Transparan"
    ]
  },
  {
    id: 5,
    name: "Kotak Perlengkapan Pancing",
    price: 195000,
    image: "/src/assets/pngwing.com.png",
    description: "Kotak penyimpanan lengkap untuk semua peralatan pancing",
    longDescription: "Kotak perlengkapan pancing dengan desain ergonomis dan tahan air. Dilengkapi dengan berbagai kompartemen yang dapat disesuaikan untuk menyimpan umpan, kail, pemberat, dan aksesori pancing lainnya dengan rapi dan terorganisir.",
    specifications: [
      "Dimensi: 35 x 22 x 15 cm",
      "Material: Plastik ABS Tahan Benturan",
      "Berat: 850 gram",
      "Jumlah Kompartemen: 15",
      "Fitur: Tahan Air, Kunci Pengaman"
    ]
  },
  {
    id: 6,
    name: "Kursi Lipat Memancing",
    price: 320000,
    image: "/src/assets/pngegg.png",
    description: "Kursi nyaman dan praktis untuk kegiatan memancing",
    longDescription: "Kursi lipat khusus untuk memancing dengan desain ergonomis dan nyaman. Dilengkapi dengan sandaran punggung, tempat minum, dan kantong penyimpanan. Mudah dibawa dan disimpan berkat desain lipatnya yang kompak.",
    specifications: [
      "Dimensi: 50 x 45 x 80 cm",
      "Material: Aluminium & Polyester",
      "Kapasitas Beban: 120 kg",
      "Berat: 2.5 kg",
      "Fitur: Sandaran, Tempat Minum, Kantong Samping"
    ]
  },
  {
    id: 7,
    name: "Jaring Pancing Lipat",
    price: 145000,
    image: "/src/assets/pngwing.com_(1).png",
    description: "Jaring pancing praktis untuk menangkap ikan hasil pancingan",
    longDescription: "Jaring pancing lipat dengan desain teleskopik yang praktis dan mudah dibawa. Ideal untuk mengangkat ikan hasil pancingan dari air. Dilengkapi dengan handle aluminium yang kuat dan ringan serta jaring yang tahan lama.",
    specifications: [
      "Panjang Handle: 1.5 meter (dapat diperpanjang)",
      "Diameter Jaring: 40 cm",
      "Material Handle: Aluminium",
      "Material Jaring: Nylon",
      "Berat: 450 gram"
    ]
  },
  {
    id: 8,
    name: "Rompi Pancing Multifungsi",
    price: 275000,
    image: "/src/assets/pngwing.com_(2).png",
    description: "Rompi dengan banyak kantong untuk perlengkapan memancing",
    longDescription: "Rompi pancing multifungsi dengan banyak kantong untuk menyimpan berbagai perlengkapan memancing. Terbuat dari bahan yang cepat kering dan nyaman dipakai. Desain yang ringan dan berventilasi baik membuat aktivitas memancing lebih nyaman.",
    specifications: [
      "Ukuran: M, L, XL, XXL",
      "Material: Polyester Quick Dry",
      "Jumlah Kantong: 14",
      "Berat: 550 gram",
      "Fitur: Tahan Air, Cepat Kering"
    ]
  },
  {
    id: 9,
    name: "Topi Pancing Anti UV",
    price: 95000,
    image: "/src/assets/pngwing.com_(3).png",
    description: "Topi perlindungan sinar UV untuk aktivitas memancing",
    longDescription: "Topi pancing dengan perlindungan UV yang optimal untuk aktivitas memancing di bawah terik matahari. Dilengkapi dengan penutup leher dan telinga yang dapat dilepas. Bahan yang cepat kering dan nyaman membuat aktivitas memancing lebih menyenangkan.",
    specifications: [
      "Ukuran: Adjustable",
      "Material: Polyester Anti UV",
      "UPF Rating: 50+",
      "Berat: 120 gram",
      "Fitur: Penutup Leher, Tali Dagu"
    ]
  }
];

const formatPrice = (price) => {
  return new Intl.NumberFormat('id-ID', {
    style: 'currency',
    currency: 'IDR'
  }).format(price);
};

const addToCart = () => {
  const cartItems = JSON.parse(localStorage.getItem('cartItems')) || [];
  const existingItem = cartItems.find(item => item.id === product.value.id);

  if (existingItem) {
    existingItem.quantity += 1;
  } else {
    cartItems.push({
      id: product.value.id,
      name: product.value.name,
      price: product.value.price,
      image: product.value.image,
      quantity: 1
    });
  }

  localStorage.setItem('cartItems', JSON.stringify(cartItems));
  updateCartCount();
  
  // Tampilkan pesan sukses
  alert('Produk berhasil ditambahkan ke keranjang!');
};

const updateCartCount = () => {
  const cartItems = JSON.parse(localStorage.getItem('cartItems')) || [];
  cartCount.value = cartItems.reduce((total, item) => total + item.quantity, 0);
};

onMounted(() => {
  const productId = parseInt(route.params.id);
  product.value = products.find(p => p.id === productId);
  
  if (!product.value) {
    router.push('/products');
  }

  updateCartCount();
});
</script>

<template>
  <div class="product-detail-page" v-if="product">
    <nav class="navbar navbar-expand-lg bg-primary navbar-dark" v-if="isProductDetailPage">
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
            <router-link to="/cart" class="btn btn-light position-relative">
              <i class="bi bi-cart"></i> Keranjang
              <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                {{ cartCount }}
              </span>
            </router-link>
          </div>
        </div>
      </div>
    </nav>

    <div class="container py-5 mt-5">
      <div class="row">
        <div class="col-md-6">
          <div class="product-image-container">
            <img :src="product.image" class="img-fluid rounded shadow" :alt="product.name">
          </div>
        </div>
        <div class="col-md-6">
          <h1 class="mb-3">{{ product.name }}</h1>
          <h3 class="text-primary mb-4">{{ formatPrice(product.price) }}</h3>
          <p class="lead mb-4">{{ product.description }}</p>
          <p class="mb-4">{{ product.longDescription }}</p>
          
          <h4 class="mb-3">Spesifikasi:</h4>
          <ul class="list-group mb-4">
            <li v-for="spec in product.specifications" :key="spec" class="list-group-item">
              <i class="bi bi-check2-circle text-primary me-2"></i>
              {{ spec }}
            </li>
          </ul>
          
          <button class="btn btn-primary btn-lg w-100" @click="addToCart">
            <i class="bi bi-cart-plus me-2"></i>
            Tambah ke Keranjang
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product-detail-page {
  background-color: #f8f9fa;
  min-height: 100vh;
}

.product-image-container {
  background-color: white;
  padding: 2rem;
  border-radius: 1rem;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  transition: all 0.3s ease;
}

.product-image-container:hover {
  transform: scale(1.02);
  box-shadow: 0 6px 16px rgba(0,0,0,0.15);
}

.list-group-item {
  border: none;
  background-color: transparent;
  padding: 0.75rem 0;
}

.btn-primary {
  padding: 1rem;
  font-size: 1.1rem;
  transition: all 0.3s ease;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(13, 110, 253, 0.3);
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1030;
  padding: 1rem 0;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}
</style>