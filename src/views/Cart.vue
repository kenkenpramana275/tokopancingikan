<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const cartItems = ref([]);
const showCheckoutForm = ref(false);
const orderSuccess = ref(false);

const customerInfo = ref({
  name: '',
  email: '',
  phone: '',
  address: '',
  notes: ''
});

const formErrors = ref({
  name: '',
  email: '',
  phone: '',
  address: ''
});

const formatPrice = (price) => {
  return new Intl.NumberFormat('id-ID', {
    style: 'currency',
    currency: 'IDR'
  }).format(price);
};

const updateQuantity = (itemId, newQuantity) => {
  const item = cartItems.value.find(item => item.id === itemId);
  if (item) {
    if (newQuantity < 1) {
      removeItem(itemId);
    } else {
      item.quantity = newQuantity;
      saveCart();
    }
  }
};

const removeItem = (itemId) => {
  const index = cartItems.value.findIndex(item => item.id === itemId);
  if (index !== -1) {
    cartItems.value.splice(index, 1);
    saveCart();
  }
};

const total = ref(0);

const updateTotal = () => {
  total.value = cartItems.value.reduce((sum, item) => sum + (item.price * item.quantity), 0);
};

const saveCart = () => {
  localStorage.setItem('cartItems', JSON.stringify(cartItems.value));
  updateTotal();
};

const validateForm = () => {
  let isValid = true;
  formErrors.value = {
    name: '',
    email: '',
    phone: '',
    address: ''
  };

  if (!customerInfo.value.name.trim()) {
    formErrors.value.name = 'Nama harus diisi';
    isValid = false;
  }

  if (!customerInfo.value.email.trim()) {
    formErrors.value.email = 'Email harus diisi';
    isValid = false;
  } else if (!/\S+@\S+\.\S+/.test(customerInfo.value.email)) {
    formErrors.value.email = 'Format email tidak valid';
    isValid = false;
  }

  if (!customerInfo.value.phone.trim()) {
    formErrors.value.phone = 'Nomor telepon harus diisi';
    isValid = false;
  }

  if (!customerInfo.value.address.trim()) {
    formErrors.value.address = 'Alamat harus diisi';
    isValid = false;
  }

  return isValid;
};

const processCheckout = () => {
  if (!validateForm()) {
    return;
  }

  // Simulasi proses checkout
  const order = {
    items: cartItems.value,
    customer: customerInfo.value,
    total: total.value,
    orderDate: new Date().toISOString(),
    orderNumber: 'ORD-' + Date.now()
  };

  // Simpan order ke localStorage untuk history (opsional)
  const orders = JSON.parse(localStorage.getItem('orders') || '[]');
  orders.push(order);
  localStorage.setItem('orders', JSON.stringify(orders));

  // Kosongkan keranjang
  cartItems.value = [];
  localStorage.removeItem('cartItems');
  
  // Tampilkan sukses
  orderSuccess.value = true;
  showCheckoutForm.value = false;
};

const startNewOrder = () => {
  orderSuccess.value = false;
  router.push('/products');
};

onMounted(() => {
  const savedCart = localStorage.getItem('cartItems');
  if (savedCart) {
    cartItems.value = JSON.parse(savedCart);
    updateTotal();
  }
});
</script>

<template>
  <div class="container py-5 mt-5">
    <!-- Tampilan Sukses -->
    <div v-if="orderSuccess" class="text-center py-5">
      <div class="success-animation mb-4">
        <i class="bi bi-check-circle-fill text-success display-1"></i>
      </div>
      <h2 class="mb-4">Pembelian Berhasil!</h2>
      <p class="lead mb-4">Terima kasih telah berbelanja di Toko Pancing.</p>
      <button @click="startNewOrder" class="btn btn-primary btn-lg">
        <i class="bi bi-shop me-2"></i>
        Belanja Lagi
      </button>
    </div>

    <!-- Tampilan Normal -->
    <div v-else>
      <h2 class="mb-4">{{ showCheckoutForm ? 'Checkout' : 'Keranjang Belanja' }}</h2>

      <!-- Form Checkout -->
      <div v-if="showCheckoutForm && cartItems.length" class="row">
        <div class="col-lg-8">
          <div class="card mb-4">
            <div class="card-body">
              <h4 class="mb-4">Informasi Pembeli</h4>
              <form @submit.prevent="processCheckout">
                <div class="mb-3">
                  <label class="form-label">Nama Lengkap*</label>
                  <input 
                    type="text" 
                    class="form-control" 
                    v-model="customerInfo.name"
                    :class="{ 'is-invalid': formErrors.name }"
                  >
                  <div class="invalid-feedback">{{ formErrors.name }}</div>
                </div>

                <div class="mb-3">
                  <label class="form-label">Email*</label>
                  <input 
                    type="email" 
                    class="form-control" 
                    v-model="customerInfo.email"
                    :class="{ 'is-invalid': formErrors.email }"
                  >
                  <div class="invalid-feedback">{{ formErrors.email }}</div>
                </div>

                <div class="mb-3">
                  <label class="form-label">Nomor Telepon*</label>
                  <input 
                    type="tel" 
                    class="form-control" 
                    v-model="customerInfo.phone"
                    :class="{ 'is-invalid': formErrors.phone }"
                  >
                  <div class="invalid-feedback">{{ formErrors.phone }}</div>
                </div>

                <div class="mb-3">
                  <label class="form-label">Alamat Lengkap*</label>
                  <textarea 
                    class="form-control" 
                    rows="3" 
                    v-model="customerInfo.address"
                    :class="{ 'is-invalid': formErrors.address }"
                  ></textarea>
                  <div class="invalid-feedback">{{ formErrors.address }}</div>
                </div>

                <div class="mb-3">
                  <label class="form-label">Catatan (Opsional)</label>
                  <textarea 
                    class="form-control" 
                    rows="2" 
                    v-model="customerInfo.notes"
                  ></textarea>
                </div>

                <div class="d-flex gap-2">
                  <button type="button" class="btn btn-outline-secondary" @click="showCheckoutForm = false">
                    <i class="bi bi-arrow-left me-2"></i>
                    Kembali
                  </button>
                  <button type="submit" class="btn btn-primary">
                    <i class="bi bi-credit-card me-2"></i>
                    Proses Pembayaran
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
        
        <div class="col-lg-4">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title mb-4">Ringkasan Pesanan</h5>
              <div class="mb-3">
                <div v-for="item in cartItems" :key="item.id" class="d-flex justify-content-between mb-2">
                  <small>{{ item.name }} ({{ item.quantity }}x)</small>
                  <small>{{ formatPrice(item.price * item.quantity) }}</small>
                </div>
              </div>
              <hr>
              <div class="d-flex justify-content-between mb-3">
                <strong>Total Pembayaran</strong>
                <strong class="text-primary">{{ formatPrice(total) }}</strong>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Tampilan Keranjang -->
      <div v-else-if="cartItems.length" class="row">
        <div class="col-lg-8">
          <div class="card mb-4">
            <div class="card-body">
              <div v-for="item in cartItems" :key="item.id" class="row mb-4">
                <div class="col-md-2">
                  <img :src="item.image" class="img-fluid rounded" :alt="item.name">
                </div>
                <div class="col-md-5">
                  <h5 class="mb-2">{{ item.name }}</h5>
                  <p class="mb-0 text-muted">{{ formatPrice(item.price) }}</p>
                </div>
                <div class="col-md-3">
                  <div class="d-flex align-items-center">
                    <button 
                      class="btn btn-outline-secondary btn-sm"
                      @click="updateQuantity(item.id, item.quantity - 1)"
                    >
                      <i class="bi bi-dash"></i>
                    </button>
                    <span class="mx-3">{{ item.quantity }}</span>
                    <button 
                      class="btn btn-outline-secondary btn-sm"
                      @click="updateQuantity(item.id, item.quantity + 1)"
                    >
                      <i class="bi bi-plus"></i>
                    </button>
                  </div>
                </div>
                <div class="col-md-2 text-end">
                  <button 
                    class="btn btn-outline-danger btn-sm"
                    @click="removeItem(item.id)"
                  >
                    <i class="bi bi-trash"></i>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <div class="col-lg-4">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title mb-4">Ringkasan Belanja</h5>
              <div class="d-flex justify-content-between mb-3">
                <span>Total Barang</span>
                <span>{{ cartItems.length }} item</span>
              </div>
              <div class="d-flex justify-content-between mb-3">
                <span>Total Harga</span>
                <strong>{{ formatPrice(total) }}</strong>
              </div>
              <button 
                class="btn btn-primary w-100 mt-3"
                @click="showCheckoutForm = true"
              >
                <i class="bi bi-credit-card me-2"></i>
                Checkout
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Keranjang Kosong -->
      <div v-else class="text-center py-5">
        <i class="bi bi-cart-x display-1 text-muted mb-4"></i>
        <h3>Keranjang Belanja Kosong</h3>
        <p class="text-muted">Silakan tambahkan produk ke keranjang</p>
        <router-link to="/products" class="btn btn-primary">
          <i class="bi bi-shop me-2"></i>
          Lihat Produk
        </router-link>
      </div>
    </div>
  </div>
</template>

<style scoped>
.success-animation {
  animation: scale-up 0.4s ease-in-out;
}

@keyframes scale-up {
  0% {
    transform: scale(0.5);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

.card {
  border: none;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.btn-primary {
  transition: all 0.3s ease;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(13, 110, 253, 0.3);
}
</style>