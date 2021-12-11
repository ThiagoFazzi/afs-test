<template>
  <div class="home">
    <h1>This is a table with some important data</h1>
    <b-table :data="tableData" :columns="columns" :row-class="highlightTotal"></b-table>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { TableData } from "@/types/types";

@Component
export default class Home extends Vue {
  tableData: TableData[] = [];
  columns = [
    {
      label: "Security class",
      field: "name",
    },
    {
      label: "Authorized amount",
      field: "authorizedAmount",
    },
    {
      label: "Issued amount",
      field: "issuedAmount",
    },
    {
      label: "Authorized Capital",
      field: "authorizedCapital",
    },
    {
      label: "Issued capital",
      field: "issuedCapital",
    },
  ];
  loading = false;

  // Task Async/Await
  async mounted() : Promise<void> {
    try {
      this.loading = true;
      const data: TableData[] = await this.getData();

      this.tableData = data.map((dataItem: TableData) : TableData => {
        return {
          ...dataItem,
          randomNumber: Math.random(),
        };
      });

      //Task Add Total Row in the table
      this.addTotal(this.tableData);

      this.loading = false;
    } catch (error) {
      console.log(error, "This is not good");
    }
  }

  // Task Add Total Row in the table
  addTotal(data: TableData[]) : void {
    const InitialObject: TableData = {
      id: "resultTotal",
      name: "Total",
      nominalValue: 0,
      authorizedAmount: 0,
      issuedAmount: 0,
      authorizedCapital: 0,
      issuedCapital: 0
    };

    const total = data.reduce((acc: TableData, curr: TableData) : TableData => {
      acc.authorizedAmount += curr.authorizedAmount;
      acc.issuedAmount += curr.issuedAmount;
      acc.authorizedCapital += curr.authorizedCapital;
      acc.issuedCapital += curr.issuedCapital;
      return acc;
    }, InitialObject);

    this.tableData = [...this.tableData, total]
  }

  // Task Add Total Row in the table
  highlightTotal(row: TableData) : string {
    console.log(row);
    return row.id === "resultTotal" ? "has-text-weight-bold" : "";
  }

  async getData(): Promise<TableData[]> {
    return [
      {
        id: "42f2462d-49d0-4e91-8fe1-de2e656b0f06",
        name: "Series A",
        nominalValue: 5,
        authorizedAmount: 1500,
        issuedAmount: 500,
        authorizedCapital: 7550,
        issuedCapital: 2500,
      },
      {
        id: "42f2462d-49d0-4e91-8fe1-de2e656b0f06",
        name: "Series B",
        nominalValue: 10,
        authorizedAmount: 15000,
        issuedAmount: 5000,
        authorizedCapital: 150000,
        issuedCapital: 50000,
      },
      {
        id: "fd78c11b-e3d2-455a-99b0-49907a75c463",
        name: "Series C",
        nominalValue: 1,
        authorizedAmount: 96876,
        issuedAmount: 61760,
        authorizedCapital: 96876,
        issuedCapital: 61760,
      },
      {
        id: "d8654cb0-8986-4fbc-b969-025e514cb934",
        name: "Series D",
        nominalValue: 1,
        authorizedAmount: 10110,
        issuedAmount: 1100,
        authorizedCapital: 10110,
        issuedCapital: 1100,
      },
    ];
  }
}
</script>
