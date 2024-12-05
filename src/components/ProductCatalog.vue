<template>
  <div class="ag-theme-alpine" style="height: 600px; width: 100%;">
    <ag-grid-vue
        :columnDefs="columnDefs"
        :rowData="rowData"
        :defaultColDef="defaultColDef"
        :pagination="true"
        :paginationPageSize="20"
        @grid-ready="onGridReady"
        class="ag-theme-alpine">
    </ag-grid-vue>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { AgGridVue } from 'ag-grid-vue3';
import 'ag-grid-community/styles/ag-grid.css';
import 'ag-grid-community/styles/ag-theme-alpine.css';

export default defineComponent({
  name: 'ProductCatalog',
  components: {
    AgGridVue,
  },
  data() {
    return {
      columnDefs: [
        {
          headerName: 'Product Name',
          field: 'productName',
          cellRenderer: this.productRenderer,
          minWidth: 250,
        },
        {
          headerName: 'Competitor 1',
          field: 'competitor1',
          minWidth: 150,
          cellRenderer: this.competitorRenderer,
        },
        { headerName: 'Suggestions', field: 'suggestions', minWidth: 150 },
        { headerName: 'Comp. URLs', field: 'compUrls', minWidth: 150 },
        { headerName: 'Brand', field: 'brand', minWidth: 100 },
        { headerName: 'Cost', field: 'cost', minWidth: 100 },
        { headerName: 'Price', field: 'price', minWidth: 100 },
        {
          headerName: 'Stock',
          field: 'stock',
          cellRenderer: this.stockRenderer,
          minWidth: 120,
        },
        { headerName: 'Min / Max Price', field: 'minMaxPrice', minWidth: 150 },
        { headerName: 'Competitor Prices', field: 'competitorPrices', minWidth: 150 },
        { headerName: 'Price Position', field: 'pricePosition', minWidth: 150 },
        {
          headerName: 'Tags',
          field: 'tags',
          cellRenderer: this.tagsRenderer,
          minWidth: 150,
        },
        {
          headerName: 'Status',
          field: 'status',
          cellRenderer: this.statusRenderer,
          minWidth: 100,
        },
      ],
      rowData: [
        {
          productName: 'Jablite Jabfloor 70',
          competitor1: { name: 'Shopify', price: 34.99, change: '-50%', status: 'In Stock' },
          suggestions: '82 Suggestions',
          compUrls: '200 URLs',
          brand: 'Zara',
          cost: 15.99,
          price: 21.19,
          stock: 'In Stock',
          minMaxPrice: 'Min: $21.15, Max: $34.99',
          competitorPrices: 'Min: $21.15, Max: $34.99',
          pricePosition: 'Lower',
          tags: ['Winter', 'Sport'],
          status: 'Active',
        },
        {
          productName: 'Jablite Jabfloor 70',
          competitor1: { name: 'Shopify', price: 34.99, change: '-50%', status: 'In Stock' },
          suggestions: '82 Suggestions',
          compUrls: '100 URLs',
          brand: 'Zara',
          cost: 15.99,
          price: 21.19,
          stock: 'In Stock',
          minMaxPrice: 'Min: $21.15, Max: $34.99',
          competitorPrices: 'Min: $21.15, Max: $34.99',
          pricePosition: 'Lower',
          tags: ['Winter', 'Sport'],
          status: 'Active',
        },
      ],
      defaultColDef: {
        sortable: true,
        filter: true,
        resizable: true,
      },
    };
  },
  methods: {
    onGridReady(params: any) {
      params.api.sizeColumnsToFit();
    },
    productRenderer(params: any) {
      return `
        <div style="display: flex; align-items: center;">
          <img src="https://via.placeholder.com/40" alt="product-image" style="margin-right: 10px;" />
          <span>${params.value}</span>
        </div>
      `;
    },
    competitorRenderer(params: any) {
      return `
        <div>
          <div><strong>${params.value.name}</strong></div>
          <div>$${params.value.price} (${params.value.change})</div>
          <div style="color: ${params.value.status === 'In Stock' ? 'green' : 'red'};">${params.value.status}</div>
        </div>
      `;
    },
    stockRenderer(params: any) {
      const color = params.value === 'In Stock' ? 'green' : 'red';
      return `<span style="color: ${color}; font-weight: bold;">${params.value}</span>`;
    },
    tagsRenderer(params: any) {
      return params.value
          .map(
              (tag: string) =>
                  `<span style="background-color: #f0f0f0; padding: 3px 5px; margin-right: 5px; border-radius: 5px;">${tag}</span>`
          )
          .join('');
    },
    statusRenderer(params: any) {
      return `<span style="color: green; font-weight: bold;">${params.value}</span>`;
    },
  },
});
</script>

<style scoped>
.ag-theme-alpine {
  height: 100%;
  width: 100%;
}
</style>