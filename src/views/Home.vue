<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="white"
      flat
    >
      <v-avatar
        :color="$vuetify.breakpoint.smAndDown ? 'grey darken-1' : 'transparent'"
        size="32"
      ></v-avatar>

      <v-tabs
        centered
        class="ml-n9"
        color="grey darken-1"
      >
        <v-tab
          v-for="link in links"
          :key="link"
        >
          {{ link }}
        </v-tab>
      </v-tabs>

      <v-avatar
        class="hidden-sm-and-down"
        color="grey darken-1 shrink"
        size="32"
      ></v-avatar>
      <span style="margin-left:10px">Ayman</span>
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
        <v-row>
          <v-col
            cols="4"
          >
            <v-sheet
              rounded="lg"
              min-height="100"
            >
              <v-row style="padding:15px">
                <v-col
                  cols="12"
                >
                  <v-date-picker
                    v-model="dates"
                    range
                  ></v-date-picker>
                </v-col>
                <v-col
                  cols="12"
                >
                  <v-text-field
                    v-model="dateRangeText"
                    label="Date range"
                    prepend-icon="mdi-calendar"
                    readonly
                  ></v-text-field>
                </v-col>
              </v-row>

            </v-sheet>
          </v-col>
          <v-col
            cols="8"
          >
            <v-sheet
              rounded="lg"
              min-height="100"
            >
              <v-row style="padding:15px">
                <v-col
                  cols="12"
                >
                <h1>Statisitcs</h1>
                </v-col>
              </v-row>

            </v-sheet>
          </v-col>
          <v-col
            cols="12"
          >
            <v-sheet
              min-height="70vh"
              rounded="lg"
            >
            <v-row>
              <v-col cols="6">
                <v-card style="margin:10px;padding:10px">
                  <h3>Total Case Detected</h3>
                  <apexchart width="475" type="donut" :options="options" :series="series"></apexchart>
                </v-card>
              </v-col>
              <v-col cols="6">
                <v-card style="margin:10px;padding:10px">
                  <h3>Chronic TTs Vs Vendor</h3>
                  <apexchart type="bar" height="350" :options="chartOptions" :series="series1"></apexchart>
                </v-card>
              </v-col>
            </v-row>
              <v-row>
              <v-col cols="6">
                <v-card style="margin:10px;padding:10px">
                  <h3>TTs Status</h3>
                  <apexchart width="500" type="donut" :options="options2" :series="series2"></apexchart>
                </v-card>
              </v-col>
            </v-row>
            <v-row>
                <v-col cols="4">
                  <v-card style="margin:10px;padding:10px">
                    <h3>Runing TTs</h3>
                    <apexchart width="280" type="donut" :options="options2" :series="series2"></apexchart>
                  </v-card>
                </v-col>
                <v-col cols="4">
                  <v-card style="margin:10px;padding:10px">
                    <h3>Resolved TTs</h3>
                    <apexchart width="280" type="donut" :options="options2" :series="series2"></apexchart>
                  </v-card>
                </v-col>
                <v-col cols="4">
                  <v-card style="margin:10px;padding:10px">
                    <h3>Pending TTs</h3>
                    <apexchart width="280" type="donut" :options="options2" :series="series2"></apexchart>
                  </v-card>
                </v-col>
            </v-row>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      links: [
        'Home',
        'Chronic Records',
      ],
      dates: [],

      //Total Case Detected
      options: {},
      series: [44, 55, 41, 17, 15],

      //Chronic TTs Vs Vendor
          series1: [{
            name: '2G',
            data: [44, 55, 41]
          }, {
            name: '3G',
            data: [13, 23, 20]
          }, {
          }],
          chartOptions: {
            chart: {
              type: 'bar',
              height: 350,
              stacked: true,
              stackType: '100'
            },
            responsive: [{
              breakpoint: 480,
              options: {
                legend: {
                  position: 'bottom',
                  offsetX: -10,
                  offsetY: 0
                }
              }
            }],
            xaxis: {
              categories: ['E///', 'Huawei', 'ZTE'
              ],
            },
            fill: {
              opacity: 1
            },
            legend: {
              position: 'right',
              offsetX: 0,
              offsetY: 50
            },
          },

          //TTs status
          options2: {},
          series2: [44, 55, 41, 17, 15],

    }),
    computed: {
      dateRangeText () {
        return this.dates.join(' ~ ')
      },
    },
  }
</script>