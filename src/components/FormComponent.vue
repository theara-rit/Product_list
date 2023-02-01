<template>
  <div class="form">
    <h2 class="mb-4 text-3xl font-bold text-blue-600">Product Form</h2>
    <form class="w-1/2 m-auto rounded-lg bg-slate-400 p-3">
      <div class="flex flex-wrap -mx-3 mb-6">
        <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
          <label class="" for="grid-city"> Name </label>
          <input
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            id="grid-city"
            type="text"
            v-model="data_form.name"
          />
        </div>
        <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
          <label class="" for="grid-zip"> Code </label>
          <input
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            id="grid-zip"
            type="number"
            v-model="data_form.code"
          />
        </div>
        <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
          <label class="" for="grid-zip"> QIY </label>
          <input
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            id="grid-zip"
            type="number"
            v-model="data_form.qiy"
          />
        </div>
      </div>
      <h3 class="flex justify-start mb-2">Stock location</h3>
      <div class="flex flex-wrap -mx-3 mb-6">
        <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
          <div class="relative">
            <select
              name=""
              id=""
              v-model="data_form.stock_location.province"
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            >
              <!-- <option value="" selected disabled>Province</option> -->
              <option
                v-for="(value, index) of provinces"
                :key="index"
                :value="value.id"
              >
                {{ value.name_latin }}
              </option>
            </select>
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
            >
              <svg
                class="fill-current h-4 w-4"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <path
                  d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                />
              </svg>
            </div>
          </div>
        </div>
        <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
          <div class="relative">
            <select
              name=""
              id=""
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              v-model="data_form.stock_location.district"
            >
              <!-- <option value="" selected disabled>District</option> -->
              <option
                v-for="(value, index) of filteredDistricts"
                :key="index"
                :value="value.id"
              >
                {{ value.name_latin }}
              </option>
            </select>
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
            >
              <svg
                class="fill-current h-4 w-4"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <path
                  d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                />
              </svg>
            </div>
          </div>
        </div>
        <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
          <div class="relative">
            <select
              name=""
              id=""
              v-model="data_form.stock_location.commune"
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            >
              <!-- <option value="" selected disabled>Commune</option> -->

              <option
                v-for="(value, index) of filteredCommune"
                :key="index"
                :value="value.id"
              >
                {{ value.name_latin }}
              </option>
            </select>
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
            >
              <svg
                class="fill-current h-4 w-4"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <path
                  d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                />
              </svg>
            </div>
          </div>
        </div>
      </div>
      <h3 class="flex justify-start mb-2">Min Purchase</h3>
      <div>
        <div
          v-for="(data, index) of data_form.min_purchase"
          :key="index"
          class="flex flex-wrap -mx-3 mb-6"
        >
          <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="grid-city"
              type="number"
              placeholder="From amount"
              v-model="data.from_amount"
            />
          </div>
          <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="grid-zip"
              type="number"
              placeholder="To amount"
              v-model="data.to_amount"
            />
          </div>

          <div class="w-full md:w-1/3 px-3 md:mb-0">
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="grid-last-name"
              type="number"
              placeholder="Price"
              v-model="data.price"
            />
          </div>
        </div>
        <div class="btn mt-3 flex justify-end">
          <Button
            class="bg-red-500 w-12 p-2 rounded text-slate-100"
            @click="onClickAddPurchase()"
          >
            <template #btn>Add</template>
          </Button>
        </div>
      </div>
      <div class="w-full px-3 mb-6 md:mb-0">
        <label for="" class="flex justify-start">Description</label>
        <textarea
          name="Description"
          id=""
          cols="30"
          rows="10"
          v-model="data_form.description"
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
        ></textarea>
      </div>
      <div class="w-full px-3 mb-6">
        <div class="img">
          <h3>image</h3>
          <div>
            <input type="file" id="file" hidden @change="onFileChange" />
          </div>
          <div
            class="bg-red-500 w-10 h-10 rounded-full text-2xl flex justify-center items-center text-white"
            for="file"
          >
            <label for="file">+</label>
          </div>
          <div class="grid grid-cols-4 gap-5 mt-10">
            <div v-for="(pic, index) of data_form.images" :key="index">
              <img :src="pic.img" alt="" />
            </div>
          </div>
        </div>
      </div>
      <div class="w-full px-3 mb-6 md:mb-0 flex justify-end">
        <Button
          class="bg-orange-500 p-2 rounded text-slate-100 mr-5"
          @click="onCancel()"
        >
          <template #btn>Cancel</template>
        </Button>
        <Button
          class="bg-blue-500 p-2 rounded text-slate-100"
          @click="onSubmit()"
        >
          <template #btn>save</template>
        </Button>
      </div>
    </form>
  </div>
</template>
<script>
import Button from "./ButtonComponent.vue";
import Province from "../Data/Province.json";
import District from "../Data/District.json";
import Commune from "../Data/Commune.json";
export default {
  props: ["itemEdit", "isEdit"],
  components: {
    Button,
  },
  data() {
    return {
      provinces: Province,
      district: District,
      communes: Commune,
      datas: [],
      data_form: {
        name: "",
        code: null,
        qiy: null,
        description: "",
        stock_location: {
          province: "",
          district: "",
          commune: "",
        },
        min_purchase: [
          {
            id: "",
            from_amount: 0,
            to_amount: 0,
            price: 0,
          },
        ],
        images: [],
      },
    };
  },
  methods: {
    onClickAddPurchase() {
      this.data_form.min_purchase.push({
        id: "",
        from_amount: 0,
        to_amount: 0,
        price: 0,
      });
    },
    onFileChange(e) {
      const file = e.target.files[0];
      let url = URL.createObjectURL(file);
      let image = {
        img: url,
      };
      this.data_form.images.push(image);
    },

    onSubmit() {
      this.$emit("data", this.data_form);
      this.$emit("currentPage", "list");
    },
    onCancel() {
      this.$emit("currentPage", "list");
    },
  },
  computed: {
    filteredDistricts() {
      return this.district.filter((dist) => {
        return dist.province_id == this.data_form.stock_location.province;
      });
    },
    filteredCommune() {
      return this.communes.filter((com) => {
        return com.district_id == this.data_form.stock_location.district;
      });
    },
  },
  mounted() {
    if (this.isEdit) {
      this.data_form = this.itemEdit[0];
    }
  },
};
</script>

<style></style>
