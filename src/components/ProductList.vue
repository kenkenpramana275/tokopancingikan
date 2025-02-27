<script setup>
import { ref, computed } from 'vue';
import { useRouter, useRoute } from 'vue-router';

const router = useRouter();
const route = useRoute();

const isProductPage = computed(() => {
  return route.path === '/products';
});

const products = ref([
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
]);

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
  <div class="container mt-4" :class="{ 'products-page': isProductPage }">
    <h2 class="mb-4" :class="{ 'text-primary text-center': isProductPage }">
      {{ isProductPage ? 'Katalog Produk Lengkap' : 'Produk Unggulan' }}
    </h2>
    <div class="row g-4">
      <div v-for="product in products" :key="product.id" 
           :class="[
             isProductPage ? 'col-lg-4 col-md-6' : 'col-md-4',
             'mb-4'
           ]">
        <div class="card product-card h-100" 
             @click="goToProduct(product.id)" 
             :class="{ 'product-card-highlight': isProductPage }">
          <div class="card-img-wrapper">
            <img :src="product.image" class="card-img-top" :alt="product.name">
          </div>
          <div class="card-body">
            <h5 class="card-title" :class="{ 'text-primary': isProductPage }">{{ product.name }}</h5>
            <p class="card-text">{{ product.description }}</p>
            <p class="card-text">
              <strong :class="{ 'text-primary': isProductPage }">{{ formatPrice(product.price) }}</strong>
            </p>
            <button class="btn w-100" :class="isProductPage ? 'btn-primary' : 'btn-outline-primary'">
              <i class="bi bi-eye me-2"></i>
              Lihat Detail
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.products-page {
  padding-top: 2rem;
  background-color: #f8f9fa;
  min-height: 100vh;
}

.product-card {
  transition: all 0.3s ease;
  border: none;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.product-card-highlight {
  border: none;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.product-card-highlight:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}

.card-img-wrapper {
  overflow: hidden;
  position: relative;
  padding-top: 66.67%; /* 3:2 Aspect Ratio */
}

.card-img-wrapper img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.product-card:hover img {
  transform: scale(1.05);
}

.card-title {
  font-weight: 600;
  margin-bottom: 1rem;
}

.btn-primary {
  transition: all 0.3s ease;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(13, 110, 253, 0.2);
}
</style>