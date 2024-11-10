<template>
    <div class="container mt-4">
      <h2 class="text-center mb-4">Show Product</h2>
      
      <div class="row">
        <!-- วนลูปแสดงสินค้าแต่ละรายการ โดยให้แสดงเป็น 4 คอลัมน์ -->
        <div v-for="product in products" :key="product.id" class="col-md-3 mb-4">
          <div class="card">
            <img :src="product.image" :alt="product.name" class="card-img-top">
            <div class="card-body text-center">
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">{{ product.price }} บาท</p>
              <button @click="addToCart(product)" class="btn btn-primary">สั่งซื้อ</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [
          { id: 1, name: 'สินค้า 1', price: '100', image: 'https://via.placeholder.com/150' },
          { id: 2, name: 'สินค้า 2', price: '200', image: 'https://via.placeholder.com/150' },
          { id: 3, name: 'สินค้า 3', price: '300', image: 'https://via.placeholder.com/150' },
          { id: 4, name: 'สินค้า 4', price: '400', image: 'https://via.placeholder.com/150' },
          { id: 5, name: 'สินค้า 5', price: '500', image: 'https://via.placeholder.com/150' },
          { id: 6, name: 'สินค้า 6', price: '600', image: 'https://via.placeholder.com/150' },
          { id: 7, name: 'สินค้า 7', price: '700', image: 'https://via.placeholder.com/150' },
          { id: 8, name: 'สินค้า 8', price: '800', image: 'https://via.placeholder.com/150' }
        ]
      };
    },
    methods: {
      addToCart(product) {
        alert(`เพิ่ม ${product.name} ลงในรถเข็นเรียบร้อยแล้ว!`);
      }
    }
  };
  </script>
  
  <style scoped>
  /* กำหนดสไตล์เพิ่มเติมสำหรับ card */
  .card {
    border: 1px solid #ddd;
    transition: box-shadow 0.3s;
  }
  .card:hover {
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
  }
  .card-img-top {
    max-height: 150px;
    object-fit: cover;
  }
  </style>
  