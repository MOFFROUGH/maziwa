<template>
  <div>
    <v-layout row wrap>
      <v-flex xs12 sm4 md4>
        <v-card class="mr-2" height="100%">
          <v-card-title>
            <h2 class="mt-2 mb-2" style="text-decoration:underline; ">Cow Profile</h2>
          </v-card-title>
          <v-card-text>
            <h3>Name: <span style="color:black;text-transform: capitalize;">{{cow.name}}</span> </h3>
            <h3>Breed: <span style="color:black;text-transform: capitalize;">{{cow.breed}}</span> </h3>
            <h3>weight: <span style="color:black;text-transform: capitalize;">{{cow.weight}}</span> </h3>
            <h3>Year of birth: <span style="color:black;text-transform: capitalize;">{{cow.date}}</span> </h3>
          </v-card-text>
          <v-card-text>
            <img class="preview mt-2" :src="cow.picture">
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex xs12 sm8 md8>
        <v-card class="mr-1">
          <!-- ---------Date picker  -------->
          <v-layout row wrap>
            <v-card-title primary-title >
              <h2 class="headline">Milk and Feed comparison of {{cow.name}}</h2>
              <!-- <h2>Milk and feeds  Chart for chelel for the last 30 day</h2> -->
            </v-card-title>
            <v-flex xs12 sm6>
              <v-menu
              ref="menu1"
              :close-on-content-click="false"
              v-model="menu1"
              :nudge-right="40"
              :return-value.sync="date1"
              lazy
              transition="scale-transition"
              offset-y
              min-width="200"
              full-width>
              <v-text-field
              slot="activator"
              v-model="date1"
              label="From"
              prepend-icon="event"
              readonly
              ></v-text-field>
              <v-date-picker v-model="date1"  no-title scrollable>
                <v-btn flat color="primary" @click="menu1 = false">Cancel</v-btn>
                <v-btn flat color="primary" @click="date_picked('menu1',date1)">OK</v-btn>
              </v-date-picker>
            </v-menu>
          </v-flex>
          <v-flex xs12 sm6>
            <v-menu
            ref="menu2"
            :close-on-content-click="false"
            v-model="menu2"
            :nudge-right="40"
            :return-value.sync="date2"
            lazy
            transition="scale-transition"
            offset-y
            full-width
            min-width="200"

            >
            <v-text-field
            slot="activator"
            v-model="date2"
            label="To"
            prepend-icon="event"
            readonly
            ></v-text-field>
            <v-date-picker v-model="date2"  no-title scrollable>
              <v-spacer></v-spacer>
              <v-btn flat color="primary" @click="menu2 = false">Cancel</v-btn>
              <v-btn flat color="primary" @click="date_picked('menu2',date2)">OK</v-btn>
            </v-date-picker>
          </v-menu>
        </v-flex>
      </v-layout>
    </v-card>
    <canvas ref="chart"/>
  </v-flex>

    <v-layout row wrap>
      <v-flex xs12 sm12>
        <v-card class="mt-2 mb-0">
          <v-card-title style="justify-content:center;"><h2 >Milk produced by {{cow.name}} in the last 30 days</h2>
          </v-card-title>
          <div>
            <v-card-title>
              {{cow.name}} milk data
              <v-spacer></v-spacer>
              <v-text-field
              v-model="search"
              append-icon="search"
              label="Search"
              single-line
              hide-details
              ></v-text-field>
            </v-card-title>
            <v-data-table
            :headers="headers"
            :items="cow_data"
            :search="search"
            >
            <template slot="items" slot-scope="props">
              <td>{{ props.item.milk }}</td>
              <td>{{ props.item.date }}</td>
            </template>
            <v-alert slot="no-results" :value="true" color="error" icon="warning">
              Your search for "{{ search }}" found no results.
            </v-alert>
          </v-data-table>
        </div>
      </v-card>
    </v-flex>
  </v-layout>
</v-flex>
</v-layout>
</div>
</template>

<script>
export default {
  props: ['slug'],
  data () {
    return {
      date1: null,
      date2: null,
      menu1: false,
      menu2: false,
      date: null,
      search: '',
      headers: [
        {
          text: 'Milk', value: 'milk'},
          { text: 'Date', value: 'date' }
        ],
        cow_data: [
          {
            milk: 30,
            date: '2018-06-09'

          },
          {
            milk: 40,
            date: '2018-05-19'
          }
        ]
      }
    },
    computed: {
      cow () {
        return this.$store.getters.getCow(this.slug)
      }
    },
    mounted() {
      // console.log(this.$store.state.cows[0])
      var chart = this.$refs.chart;
      var ctx = chart.getContext("2d");
      var myChart = new Chart(ctx, {
        type: "line",
        data: {
          labels: ["January", "February", "March", "April", "May", "June", "July"],
          datasets: [
            {
              label: "Feeds",
              data: [65, 59, 80, 81, 56, 55, 40],
              backgroundColor: [

                'rgba(54,73,93,.5)', // Blue
                'rgba(54,73,93,.5)',
                'rgba(255,0,0,.5)',
                'rgba(54,73,93,.5)',
                'rgba(54,73,93,.5)',
                'rgba(54,73,93,.5)',
                'rgba(54,73,93,.5)',
                'rgba(54,73,93,.5)'
              ],
              borderColor: [
                '#5600ff',
              ],
              borderWidth: 1
            },
            {
              label: "Milk",
              data: [28, 48, 40, 19, 86, 27, 90],
              backgroundColor: [
                'rgba(71, 183,132,.5)',
              ],
              borderColor: [
                '#47b784',
              ],
              borderWidth: 1
            }
          ],
          options: {
            scales: {
              yAxes: [
                {
                  ticks: {
                    beginAtZero: true
                  }
                }
              ]
            }
          }
        }
      });
    }
  }
  </script>


  <style scoped>
  img.preview {
    max-width: 90%;
    max-height: 80%;
    background-color: grey;
    border: 1px solid #ddd;
  }
  h3{
    color:rgb(14, 134, 64);
    margin-bottom: 3%
  }
  h2{
    text-align:center;
    color:green;
  }

  </style>
