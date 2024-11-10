<template>
    <div class="container vh-100 col-md-4">
      <br>
      <h2>{{ isEditing ? "แก้ไขข้อมูลสินค้า" : "เพิ่มข้อมูลสินค้า" }}</h2>
      <form @submit.prevent="isEditing ? updateProduct() : addProduct()">
        <div class="text-start">
          <label for="name">ชื่อสินค้า:</label>
          <input v-model="newProduct.name" id="name" ref="nameInput" class="form-control" required />
        </div>
        <div class="text-start">
          <label for="price">ราคา:</label>
          <input type="number" v-model="newProduct.price" id="price" class="form-control" required />
        </div>
        <div class="text-start">
          <label for="quantity">จำนวนสินค้า:</label>
          <input type="number" v-model="newProduct.quantity" id="quantity" class="form-control" required />
        </div>
        <button type="submit" class="btn btn-primary my-4">
          {{ isEditing ? "บันทึกการแก้ไข" : "เพิ่มสินค้า" }}
        </button>
        <button v-if="isEditing" @click="cancelEdit" type="button" class="btn btn-secondary my-4 ms-2">ยกเลิก</button>
      </form>
  
      <!-- แสดงรายการสินค้า -->
      <h2 v-if="products.length > 0">รายการสินค้า</h2>
      <table v-if="products.length > 0">
        <thead>
          <tr>
            <th>ชื่อสินค้า</th>
            <th>ราคา</th>
            <th>จำนวน</th>
            <th>การจัดการ</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(product, index) in products" :key="index">
            <td>{{ product.name }}</td>
            <td>{{ product.price }}</td>
            <td>{{ product.quantity }}</td>
            <td>
              <button @click="editProduct(index)" class="btn btn-warning btn-sm">แก้ไข</button>
              <button @click="deleteProduct(index)" class="btn btn-danger btn-sm ms-2">ลบ</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  
  export default {
    setup() {
      const products = ref([]); // ตัวแปรเก็บรายการสินค้า
      const newProduct = ref({ name: '', price: 0, quantity: 0 }); // เพิ่มฟิลด์ quantity ในสินค้าใหม่
      const nameInput = ref(null); // ใช้สำหรับอ้างถึงช่องกรอกชื่อสินค้าเพื่อจัดการโฟกัส
      const isEditing = ref(false); // ตัวแปรสถานะแก้ไข
      const editIndex = ref(null); // ตัวแปรเก็บ index ของสินค้าที่กำลังแก้ไข
  
      const addProduct = () => {
        if (newProduct.value.name && newProduct.value.price && newProduct.value.quantity) {
          products.value.push({ ...newProduct.value }); // เพิ่มสินค้าใหม่ในรายการสินค้า
          resetForm();
        }
      };
  
      const editProduct = (index) => {
        isEditing.value = true;
        editIndex.value = index;
        newProduct.value = { ...products.value[index] }; // คัดลอกข้อมูลสินค้าเพื่อแก้ไข
        nameInput.value.focus();
      };
  
      const updateProduct = () => {
        if (newProduct.value.name && newProduct.value.price && newProduct.value.quantity) {
          products.value[editIndex.value] = { ...newProduct.value }; // อัปเดตสินค้า
          resetForm();
        }
      };
  
      const deleteProduct = (index) => {
        products.value.splice(index, 1); // ลบสินค้าที่เลือก
      };
  
      const cancelEdit = () => {
        resetForm();
      };
  
      const resetForm = () => {
        newProduct.value = { name: '', price: 0, quantity: 0 }; // ล้างข้อมูลฟอร์ม
        isEditing.value = false;
        editIndex.value = null;
        nameInput.value.focus();
      };
  
      onMounted(() => {
        nameInput.value.focus(); // จัดการโฟกัสที่ช่องกรอกชื่อสินค้าเมื่อติดตั้งองค์ประกอบ
      });
  
      return {
        products,
        newProduct,
        isEditing,
        addProduct,
        editProduct,
        updateProduct,
        deleteProduct,
        cancelEdit,
        nameInput,
      };
    },
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    border: 1px solid #ccc;
    padding: 8px;
    text-align: left;
  }
  </style>
  