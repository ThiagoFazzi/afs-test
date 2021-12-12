<template>
  <div class="home">
    <h1>This is a table with some important data</h1>
    <b-table :data="tableData" :columns="columns" :row-class="highlightTotal"></b-table>

    <button @click="showModal = true">Add New Item</button>

    <modal v-if="showModal" @close="showModal = false">
      <div slot="header">
        <h1>Add New Item</h1>
      </div>
      
      <template slot="body">
        <form class="form">
            <div>
              <label class="form__label">Security Class</label>
              <input name="security-class" type="text" v-model="newItem.name" class="form__input"/>
            </div>

            <div>
              <label class="form__label">Authorized Amount</label>
              <input name="authorized-amount" type="number" v-model="newItem.authorizedAmount" class="form__input"/>
            </div>

            <div>
              <label class="form__label">Issued Amount</label>
              <input name="issued-amount" type="number" v-model="newItem.issuedAmount" class="form__input"/>
            </div>

            <div>
              <label class="form__label">Authorized Capital</label>
              <input name="authorized-capital" type="number" v-model="newItem.authorizedCapital" class="form__input"/>
            </div>

            <div>
              <label class="form__label">Issued Capital</label>
              <input name="issued-capital" type="number" v-model="newItem.issuedCapital" class="form__input"/>
            </div>
        </form>
      </template>

      <button slot="footer" @click="addNewItem">Add</button>

    </modal>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { TableData } from "@/types/types";
import Modal from '@/components/Modal.vue';

@Component({ components: { Modal }})
export default class Home extends Vue {
  tableData: TableData[] = [];
  columns = [
    {
      label: "Security Class",
      field: "name",
    },
    {
      label: "Authorized Amount",
      field: "authorizedAmount",
    },
    {
      label: "Issued Amount",
      field: "issuedAmount",
    },
    {
      label: "Authorized Capital",
      field: "authorizedCapital",
    },
    {
      label: "Issued Capital",
      field: "issuedCapital",
    },
  ];
  loading = false;
  showModal = false;
  newItem = {
    id: '',
    name: '',
    nominalValue: 0,
    authorizedAmount: 0,
    issuedAmount: 0,
    authorizedCapital: 0,
    issuedCapital: 0,
  };

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
      console.log(error, 'This is not good');
    }
  }

  // Task Add Total Row in the table
  /**
   * @description Validate if name filed is filled
   */
  get validateForm() : boolean {
    return !!this.newItem.name
  }

  // Task Add Total Row in the table
  /**
   * @description Update total values
   */
  addTotal(data: TableData[]) : void {
    const InitialObject: TableData = {
      id: 'resultTotal',
      name: 'Total',
      nominalValue: 0,
      authorizedAmount: 0,
      issuedAmount: 0,
      authorizedCapital: 0,
      issuedCapital: 0
    };

    const total = data.reduce((acc: TableData, curr: TableData) : TableData => {
      acc.authorizedAmount += +curr.authorizedAmount;
      acc.issuedAmount += +curr.issuedAmount;
      acc.authorizedCapital += +curr.authorizedCapital;
      acc.issuedCapital += +curr.issuedCapital;
      return acc;
    }, InitialObject);

    this.tableData = [...this.tableData, total]
  }

  // Task Add Total Row in the table
  /**
   * @description Bold the totals
   */
  highlightTotal(row: TableData) : string {
    return row.id === 'resultTotal' ? 'has-text-weight-bold' : '';
  }

  // Task Add Total Row in the table
  /**
   * @description Clean form
   */
  cleanModal() : void {
    this.newItem = {
      id: '',
      name: '',
      nominalValue: 0,
      authorizedAmount: 0,
      issuedAmount: 0,
      authorizedCapital: 0,
      issuedCapital: 0
    }
  }

  // Task Add Total Row in the table
  /**
   * @description Add new item in the table
   */
  addNewItem() : void {
    if (this.validateForm) {
      const tableDataWithoutTotal = this.tableData.filter((item) => {
        return item.id !== 'resultTotal';
      });
      this.tableData = [...tableDataWithoutTotal, this.newItem];
      this.addTotal(this.tableData);
      this.cleanModal();
      this.showModal = false;
    }
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

<style scoped lang="scss">
@import '@/assets/styles/base.scss';
</style>
