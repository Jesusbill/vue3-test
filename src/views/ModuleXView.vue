<template>
  <div class="module-x">
    <v-container class="module-x">
      <v-row align="center" justify="center">
        <v-col>
          <h1>Module X</h1>
          <v-text-field v-model="inputA" label="Enter a"></v-text-field>
          <v-text-field v-model="inputB" label="Enter b"></v-text-field>
          <v-row>
            <v-col>
              <v-btn color="primary" @click="calculateSum">Calculate</v-btn>
            </v-col>
            <v-col>
              <v-chip>Result: {{ result }}</v-chip>
            </v-col>
            <v-col>
              <v-row class="chip"
                ><v-btn :disabled="!htmlReportUrl" :href="htmlReportUrl" download="report.html"
                  ><v-icon left>mdi-download</v-icon>HTML Report</v-btn
                ></v-row
              >
              <v-row class="chip"
                ><v-btn :disabled="!pdfReportUrl" :href="pdfReportUrl" download="report.pdf"
                  ><v-icon left>mdi-download</v-icon>PDF Report</v-btn
                ></v-row
              >
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import jsPDF from 'jspdf'

const htmlReportUrl = ref(null)
const pdfReportUrl = ref(null)
const inputA = ref(0)
const inputB = ref(0)
const result = ref(0)

const calculateSum = () => {
  result.value = Number(inputA.value) + Number(inputB.value)
  createHTMLReport()
  createPDFReport()
}

const createHTMLReport = () => {
  const htmlContent = `<p>Result: ${result.value}</p>`
  const blob = new Blob([htmlContent], { type: 'text/html' })
  htmlReportUrl.value = URL.createObjectURL(blob)
}

const createPDFReport = () => {
  const doc = new jsPDF()
  doc.text(`Result: ${result.value}`, 10, 10)
  const pdfBlob = doc.output('blob')
  pdfReportUrl.value = URL.createObjectURL(pdfBlob)
}
</script>

<style>
.chip {
  margin: 5px;
}

@media (min-width: 1024px) {
  .module-x {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
