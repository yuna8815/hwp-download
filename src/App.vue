<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col class="d-flex align-center">
            <h1>Js방식으로 HWP 파일 다운로드하기</h1>
            <v-btn
              depressed
              color="primary"
              class="ml-4"
              @click="doDownload">
              다운로드
            </v-btn>
          </v-col>
        </v-row>
        <v-row>
          <v-col><Form :params="$data.model"/></v-col>
          <v-col>
            <v-textarea v-model="table" outlined />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Form from './components/Form';

export default {
  name: 'App',

  components: {
    Form
  },

  data: () => ({
    model: {},
    table: null
  }),
  methods: {
    doDownload() {
      this.sourceHTML();

      var header = `
        <html><head><meta charset='utf-8'></head><body>
        <h1>${this.$props.params.title}</h1>\n`;
      var footer = "</body></html>";
      var sourceHTML = header+this.table+footer;

      var source = 'data:application/vnd.ms-word;charset=utf-8,' + encodeURIComponent(sourceHTML);
      var fileDownload = document.createElement("a");
      document.body.appendChild(fileDownload);
      fileDownload.href = source;
      fileDownload.download = 'hi098123file.hwp';
      fileDownload.click();
      document.body.removeChild(fileDownload);
    },
    sourceHTML() {
      this.table = `<table border="1">\n\t
      <th>리스트명</th>\n\t
      ${this.createRows()}
      </table>`;
    },
    createRows() {
      let rows = '';
      this.model.lists.forEach(el => rows += `<tr>\n\t\t<td>${el}</td>\n\t</tr>\n\t`)
      return rows;
    }
  }
};
</script>
