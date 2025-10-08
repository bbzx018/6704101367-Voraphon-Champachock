<template>
  <q-page class="q-pa-md">
    <div class="q-pa-md q-gutter-md" style="max-width: 400px; margin: 0 auto;">
      <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">

        <q-input
          filled
          v-model="name"
          label="ชื่อผู้ใช้"
          hint="กรอกชื่อของคุณ"
          lazy-rules
          :rules="[ val => val && val.length > 0 || 'กรุณากรอกชื่อ' ]"
        />

        <q-input
          filled
          type="email"
          v-model="email"
          label="อีเมล"
          hint="กรอกอีเมลให้ถูกต้อง"
          lazy-rules
          :rules="[ val => val && val.includes('@') || 'อีเมลไม่ถูกต้อง' ]"
        />

        <q-select
          filled
          v-model="role"
          :options="roles"
          label="บทบาท"
        />

        <q-toggle
          v-model="subscribe"
          label="รับข่าวสารทางอีเมล"
        />

        <div class="row justify-center q-gutter-sm">
          <q-btn label="ส่งข้อมูล" type="submit" color="primary" />
          <q-btn label="ล้างฟอร์ม" type="reset" color="secondary" flat />
        </div>
      </q-form>

      <div class="q-mt-lg">
        <q-card v-if="submitted">
          <q-card-section>
            <div class="text-h6">ข้อมูลที่ส่ง:</div>
            <div>ชื่อ: {{ name }}</div>
            <div>อีเมล: {{ email }}</div>
            <div>บทบาท: {{ role }}</div>
            <div>รับข่าวสาร: {{ subscribe ? 'ใช่' : 'ไม่ใช่' }}</div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const name = ref('');
const email = ref('');
const role = ref(null);
const subscribe = ref(false);
const submitted = ref(false);

const roles = [
  'นักศึกษา',
  'อาจารย์',
  'เจ้าหน้าที่',
  'บุคคลทั่วไป'
];

function onSubmit() {
  submitted.value = true;
}

function onReset() {
  name.value = '';
  email.value = '';
  role.value = null;
  subscribe.value = false;
  submitted.value = false;
}
</script>
