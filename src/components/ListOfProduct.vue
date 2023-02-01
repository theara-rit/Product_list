<template>
  <div class="main">
    <div v-if="currentPage === 'form'">
      <FormComponent
        @data="getData"
        @currentPage="setCurrentPage"
        :itemEdit="itemEdit"
        :isEdit="isEdit"
      ></FormComponent>
    </div>

    <div class="list_of_Product" v-if="currentPage === 'list'">
      <div class="w-9/12 mx-auto">
        <div class="flex justify-end">
          <button
            @click="onAddNewItem()"
            class="bg-sky-500 hover:bg-sky-600 text-white uppercase px-5 py-2 active:translate-y-[2px] hover:translate-y-[1px] transition duration-75 ease-in-out rounded-md shadow-lg active:shadow-sm shadow-sky-300 ml-3"
          >
            Add
          </button>
        </div>
        <div class="overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="py-4 inline-block min-w-full sm:px-6 lg:px-8">
            <div class="overflow-hidden">
              <table class="min-w-full text-center border">
                <thead class="border-b bg-gray-800">
                  <tr>
                    <th
                      scope="col"
                      class="text-sm font-medium text-white px-6 py-4"
                    >
                      #
                    </th>
                    <th
                      scope="col"
                      class="text-sm font-medium text-white px-6 py-4"
                    >
                      Product Name
                    </th>
                    <th
                      scope="col"
                      class="text-sm font-medium text-white px-6 py-4"
                    >
                      Product Code
                    </th>
                    <th
                      scope="col"
                      class="text-sm font-medium text-white px-6 py-4"
                    >
                      Quantity
                    </th>
                    <th
                      scope="col"
                      class="text-sm font-medium text-white px-6 py-4"
                    >
                      Stock Location
                    </th>
                    <th
                      scope="col"
                      class="text-sm font-medium text-white px-6 py-4"
                    >
                      Actions
                    </th>
                  </tr>
                </thead>
                <tbody v-for="(item, index) of datas" :key="index">
                  <tr class="bg-white border-b">
                    <td
                      class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900"
                    >
                      {{ index + 1 }}
                    </td>
                    <td
                      class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                    >
                      {{ item.name }}
                    </td>
                    <td
                      class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                    >
                      {{ item.code }}
                    </td>
                    <td
                      class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                    >
                      {{ item.qiy }}
                    </td>
                    <td
                      class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                    >
                      {{ item.stock_location.province }}
                    </td>
                    <td
                      class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                    >
                      <button
                        @click="onEdit(item.id)"
                        class="bg-green-500 hover:bg-green-600 text-white uppercase p-2 ml-2 active:translate-y-[2px] hover:translate-y-[1px] transition duration-75 ease-in-out rounded-md shadow-lg active:shadow-sm shadow-green-300"
                      >
                        Edit
                      </button>
                      <button
                        @click="onDeleteItem(item.id)"
                        class="bg-red-500 hover:bg-red-600 text-white uppercase p-2 active:translate-y-[2px] hover:translate-y-[1px] transition duration-75 ease-in-out rounded-md shadow-lg active:shadow-sm shadow-red-300 ml-3"
                      >
                        Delete
                      </button>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FormComponent from "./FormComponent.vue";
export default {
  components: {
    FormComponent,
  },
  data() {
    return {
      currentPage: "list",
      datas: [
        {
          id: "1",
          name: "Coca",
          code: "001",
          qiy: 2,
          description: "it nice one",
          stock_location: {
            province: "01",
            district: "0102",
            commune: "010207",
          },
          min_purchase: [
            {
              id: "1",
              from_amount: 200,
              to_amount: 400,
              price: 300,
            },
          ],
          images: [
            {
              img: "https://cdn.pixabay.com/photo/2022/10/12/20/31/flower-7517474_960_720.jpg",
            },
            {
              img: "https://cdn.pixabay.com/photo/2013/07/21/13/00/rose-165819__180.jpg",
            },
            {
              img: "https://cdn.pixabay.com/photo/2013/04/03/21/25/flower-100263_960_720.jpg",
            },
          ],
        },
      ],
      itemEdit: {},
      isEdit: false,
    };
  },
  methods: {
    onAddNewItem() {
      this.isEdit = false;
      this.currentPage = "form";
    },
    getData(childData) {
      if (this.isEdit){
        console.log(childData)
        const id = childData.id;
        this.datas.map((data)=>{
          if (data.id === id){
            data = childData;
          }
        })
      }else {
        this.datas.push(childData);
      }
    },
    setCurrentPage(current) {
      this.currentPage = current;
    },
    onDeleteItem(id) {
      this.datas = this.datas.filter((data) => data.id !== id);
    },
    onEdit(id) {
      this.itemEdit = this.datas.filter((data) => data.id === id);
      this.isEdit = true;
      this.currentPage = "form";
    },
  },
  computed: {
    getItemEdit() {
      return this.itemEdit;
    },
  },
};
</script>

<style scoped></style>
