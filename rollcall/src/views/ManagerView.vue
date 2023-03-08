<template>
  <div>
    <h2>匯入Excel</h2>
    <input type="file" @change="handleFileSelect" />

    <h2>匯入結果</h2>
    <table>
      <thead>
        <tr>
          <th v-for="(value, key) in jsonData[0]" :key="key">{{ key }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) in jsonData" :key="index">
          <td v-for="(value, key) in row" :key="key">{{ value }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import XLSX from 'xlsx';

export default {
  data() {
    return {
      jsonData: [],
    };
  },
  methods: {
    handleFileSelect(event) {
      const file = event.target.files[0];

      /* 使用JS-XLSX庫解析Excel文件 */
      const reader = new FileReader();
      reader.onload = (e) => {
        const data = new Uint8Array(e.target.result);
        const workbook = XLSX.read(data, { type: 'array' });
        const worksheet = workbook.Sheets[workbook.SheetNames[0]];
        this.jsonData = XLSX.utils.sheet_to_json(worksheet, { header: 1 });
      };
      reader.readAsArrayBuffer(file);
    },
  },
};
</script>
