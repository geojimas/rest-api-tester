<template>
  <div class="layout">
    <el-container class="animate__animated animate__fadeIn">
      <el-header>
        <p>REST API Tester</p>
        <a href="https://github.com/geojimas" target="_BLANK">Github</a>
      </el-header>
      <el-main>
        <el-input minlength="1" v-model="input" placeholder="http://localhost:3000" size="large" />
        <el-button @click="onSubmit" type="primary">SENT</el-button>
      </el-main>
      <el-footer>
        <div class="card">
          <div class="demo-collapse">
            <el-collapse v-model="sectionName">
              <el-collapse-item name="1">
                <div class="result">
                  <p v-if="result === null">No Data</p>
                  <p class="animate__animated animate__fadeInDown" v-else>{{ result }}</p>
                </div>
              </el-collapse-item>
            </el-collapse>
          </div>
        </div>
      </el-footer>
    </el-container>
  </div>
</template>

<script lang="ts" setup>
import axios from 'axios'
import { ref } from 'vue'

const input = ref<string>('')
const result = ref<string | null>(null)

const sectionName = ref<string[]>(['1'])

function onSubmit(): void {
  if (input.value !== null && input.value !== '') {
    axios
      .get(input.value, {
        headers: {
          'content-type': 'application/json',
          'X-Requested-With': 'XMLHttpRequest'
        }
      })
      .then(response => {
        result.value = response.data
      })
      .catch(error => {
        result.value = error
      })
  }
}
</script>
