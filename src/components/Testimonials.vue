<script setup lang="ts">
interface Testimonial {
  id: number;
  name: string;
  image: string;
  comment: string;
  rating: number;
}

const testimonials = [
  {
    id: 1,
    name: "Budi Santoso",
    image: "https://placehold.co/100x100",
    comment: "Alat pancing yang berkualitas tinggi dan pelayanan yang sangat memuaskan!",
    rating: 5
  },
  {
    id: 2,
    name: "Ahmad Hidayat",
    image: "https://placehold.co/100x100",
    comment: "Harga terjangkau dan produknya asli. Recommended banget!",
    rating: 5
  },
  {
    id: 3,
    name: "Dewi Kusuma",
    image: "https://placehold.co/100x100",
    comment: "Pengiriman cepat dan barang sesuai dengan deskripsi.",
    rating: 4
  }
];
</script>

<template>
  <section class="bg-light py-5 mt-5">
    <div class="container">
      <h2 class="text-center mb-5">Apa Kata Pelanggan Kami</h2>
      <div class="row g-4">
        <div v-for="testimonial in testimonials" :key="testimonial.id" class="col-md-4">
          <div class="card h-100">
            <div class="card-body text-center">
              <img :src="testimonial.image" class="rounded-circle mb-3" alt="Customer Photo" width="80">
              <h5 class="card-title">{{ testimonial.name }}</h5>
              <div class="mb-2">
                <i v-for="star in testimonial.rating" :key="star" class="bi bi-star-fill text-warning"></i>
              </div>
              <p class="card-text">{{ testimonial.comment }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>