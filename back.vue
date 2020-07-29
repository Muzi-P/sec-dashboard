<template>
  <ValidationObserver ref="observer">
    <div id="app">
      <v-app id="inspire">
        <v-container
          fluid
        >
          <v-row>
            <v-btn
              class="ml-2"
              color="secondary"
              @click="toExcell"
            >
              to excell
            </v-btn>
          </v-row>
          <v-row
            no-gutters
          >
            <v-col cols="2">
              <v-card
                class="pa-5"
                outlined
                tile
              />
            </v-col>
            <v-col
              cols="10"
            >
              <v-card
                class="pa-2"
                outlined
                style="text-align: center"
              >
                A.檔案量
              </v-card>
            </v-col>
          </v-row>

          <v-row
            class="mt-n3"
          >
            <v-col>
              <v-card outlined>
                <v-data-table
                  id="mytable"
                  ref="mytable"
                  :headers="headers"
                  :items="archives"
                  :data="archives"
                  hide-default-footer
                  disable-pagination
                >
                  <template
                    v-slot:item.name="{ item }"
                  >
                    <span v-html="item.name" />
                  </template>
                  <template
                    v-slot:item.paperLength="{ item }"
                  >
                    <v-card-text style="height: 65px; width: 250px">
                      <v-row>
                        <v-col
                          class="ml-8"
                        >
                          <ValidationProvider
                            v-slot="{ errors }"
                            :rules="{ regex: /^[\u4e00-\u9fa5_a-zA-Z0-9]+$/ }"
                          >
                            <v-text-field
                              v-model="item.paperLength"
                              class="mt-n8 ml-16"
                              :error-messages="errors"
                            />
                          </ValidationProvider>
                        </v-col>
                      </v-row>
                    </v-card-text>
                  </template>
                  <template
                    v-slot:item.photoLength="{ item }"
                  >
                    <v-card-text style="height: 65px; width: 250px">
                      <v-row>
                        <v-col class="ml-8">
                          <ValidationProvider
                            v-slot="{ errors }"
                            :rules="{ regex: /^[\u4e00-\u9fa5_a-zA-Z0-9]+$/ }"
                          >
                            <v-text-field
                              v-model="item.photoLength"
                              class="mt-n8 ml-16"
                              :error-messages="errors"
                            />
                          </ValidationProvider>
                        </v-col>
                      </v-row>
                    </v-card-text>
                  </template>
                  <template
                    v-slot:item.videoLength="{ item }"
                  >
                    <v-card-text style="height: 65px; width: 250px">
                      <v-row>
                        <v-col class="ml-8">
                          <ValidationProvider
                            v-slot="{ errors }"
                            :rules="{ regex: /^[\u4e00-\u9fa5_a-zA-Z0-9]+$/ }"
                          >
                            <v-text-field
                              v-model="item.videoLength"
                              class="mt-n8 ml-16"
                              :error-messages="errors"
                            />
                          </ValidationProvider>
                        </v-col>
                      </v-row>
                    </v-card-text>
                  </template>
                  <template
                    v-slot:item.mediumLength="{ item }"
                  >
                    <v-card-text style="height: 65px; width: 250px">
                      <v-row>
                        <v-col class="ml-8">
                          <ValidationProvider
                            v-slot="{ errors }"
                            :rules="{ regex: /^[\u4e00-\u9fa5_a-zA-Z0-9]+$/ }"
                          >
                            <v-text-field
                              v-model="item.mediumLength"
                              class="mt-n8 ml-16"
                              :error-messages="errors"
                            />
                          </ValidationProvider>
                        </v-col>
                      </v-row>
                    </v-card-text>
                  </template>
                </v-data-table>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-app>
    </div>
  </ValidationObserver>
</template>
<script>
import XLSX from 'xlsx'
export default {
  name: 'ManageCollection',
  props: {
    headers: {
      type: Array,
      required: true
    },
    archives: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
    }
  },
  computed: {
    computedHeaders () {
      return this.headers.filter((item, index, array) => {
        return !item.hidden
      })
    }
  },
  methods: {
    parseInteger (item) {
      return item
    },
    toExcell () {
      console.log(this.$refs.mytable.$el)
      var wb = XLSX.utils.table_to_book(this.$refs.mytable.$el)
      XLSX.writeFile(wb, 'book.xlsx')

      // var questionWS = XLSX.utils.json_to_sheet(this.archives)
      // var wb = XLSX.utils.book_new()

      // XLSX.utils.book_append_sheet(wb, questionWS, 'animals')
      // XLSX.writeFile(wb, 'book.xlsx')
    }
  }
}
</script>
