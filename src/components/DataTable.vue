<template>
  <v-card flat>
    <v-card-title class="title font-weight-light datatable white--text">
      <v-icon color="white" class="mr-3">table_chart</v-icon>
      <span>Data Table</span>
      <v-spacer></v-spacer>
      <v-icon color="white" @click="close">close</v-icon>
    </v-card-title>
    <v-data-table class="elevation-2" :headers="headers" :items="dataset" :rows-per-page-items="[5, 10, 25]">
      <template slot="items" slot-scope="props">
        <td v-bind:key="row" v-for="(row, idx) in columns">{{ props.item[idx] }}</td>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
  import { EventBus } from '../plugins/event-bus.js';

  export default {
    props: {
      columns: Array,
      dataset: Array
    },
    computed: {
      headers() {
        let headers = [];
        if (this.dataset == []) {
          return [];
        } else {
          this.columns.forEach((val, idx) => {
            headers.push({ text: val, value: idx, sortable: false });
          });
          return headers;
        }
      }
    },
    methods: {
      close() {
        EventBus.$emit('close', 0);
      }
    }
  }
</script>