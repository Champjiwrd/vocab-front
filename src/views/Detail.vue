<template>
  <v-container>
    <div>
      <h1 class="text-center">Set {{ $route.query.day }}</h1>
      <v-card class="pa-2 elevation-10 mt-4">
        <v-table>
          <thead>
            <tr>
              <th>English</th>
              <th></th>
              <th>Thai</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(vocab, index) in vocabs" :key="index">
              <td>{{ vocab.eng }}</td>
              <td>
                <v-chip class="ma-2" color="green" text-color="white">
                  {{ vocab.part }}
                </v-chip>
              </td>
              <td>{{ vocab.tha }}</td>
            </tr>
          </tbody>
        </v-table>
      </v-card>
    </div>
    <div class="mt-4">
      <!-- <v-btn color="" disabled block>TEST</v-btn> -->
    </div>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      vocabs: [
        {
          eng: "Test",
          tha: "ทดสอบ",
        },
        {
          eng: "Test2",
          tha: "ทดสอบ",
        },
      ],
    };
  },
  mounted() {
    console.log("mounted");
    this.getVocab();
  },
  methods: {
    getVocab() {
      console.log(this.$route.query.day);
      let file = `../src/assets/vocabulary/${this.$route.query.day}.csv`;
      this.readTextFile(file);
    },
    readTextFile(file) {
      var self = this;
      self.vocabs = [];
      var rawFile = new XMLHttpRequest();
      rawFile.open("GET", file, false);
      rawFile.onreadystatechange = function () {
        if (rawFile.readyState === 4) {
          if (rawFile.status === 200 || rawFile.status == 0) {
            var allText = rawFile.responseText.split("\r\n");
            for (let index = 1; index < allText.length; index++) {
              console.log(allText[index]);
              const element = allText[index].split(",");
              console.log(element);
              self.vocabs.push({
                id: element[0],
                eng: element[1],
                part: element[2],
                tha: element
                  .slice(3)
                  .map((str) => str.replace(/"/g, ""))
                  .join(","),
              });
            }
            console.log(self.vocabs);
          }
        }
      };
      rawFile.send(null);
    },
  },
};
</script>

<style></style>
