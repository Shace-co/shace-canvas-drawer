<template>
  <div>
    <Modal v-model="showPricingForm" :title="hello" @on-ok="createRoom">
      <div>
        <label for="room_name" class="text-white">Room Name</label>
        <input
          type="text"
          name="room_name"
          v-model="form.room_name"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          id="room_name"
        />
      </div>
      <div>
        <label for="room_desc" class="text-white">Room Description</label>
        <textarea
          name="room_desc"
          v-model="form.room_desc"
          id="room_desc"
          cols="30"
          rows="10"
        ></textarea>
      </div>
      <div>
        <label for="hourly_price" class="text-white">Hourly Price</label>
        <input
          type="number"
          name="hourly_price"
          v-model="form.hourly_price"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          id="hourly_price"
        />
      </div>
      <div>
        <label for="daily_price" class="text-gray-900">Daily Price</label>
        <input
          type="number"
          v-model="form.daily_price"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="daily_price"
          id="daily_price"
        />
      </div>
      <div>
        <label for="monthly_price" class="text-gray-900">Monthly Price</label>
        <input
          type="number"
          v-model="form.monthly_price"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="monthly_price"
          id="monthly_price"
        />
      </div>
      <div>
        <label for="quarterly_price" class="text-gray-900">Quarterly Price</label>
        <input
          type="number"
          v-model="form.quarterly_price"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="quarterly_price"
          id="monthly_price"
        />
      </div>
      <div>
        <label for="semiAnnual_price" class="text-gray-900">Semi Annual Price</label>
        <input
          type="number"
          v-model="form.semiAnnual_price"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="semiAnnual_price"
          id="monthly_price"
        />
      </div>
      <div>
        <label for="yearly_price" class="text-gray-900">Yearly Price</label>
        <input
          type="number"
          v-model="form.yearly_price"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="yearly_price"
          id="yearly_price"
        />
      </div>
      <div>
        <label for="hourly_adjusment" class="text-gray-900">Hourly Adjustment</label>
        <input
          type="number"
          v-model="form.hourly_adjusment"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="hourly_adjusment"
          id="hourly_adjusment"
        />
      </div>
      <div>
        <label for="daily_adjustment" class="text-gray-900">Daily Adjustment</label>
        <input
          type="text"
          v-model="form.daily_adjustment"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="daily_adjustment"
          id="daily_adjustment"
        />
      </div>

      <div>
        <label for="monthly_adjustment" class="text-gray-900">Monthly Adjustment</label>
        <input
          type="text"
          v-model="form.monthly_adjustment"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="monthly_adjustment"
          id="monthly_adjustment"
        />
      </div>
      <div>
        <label for="quarterly_adjustment" class="text-gray-900">Quarterly Adjustment</label>
        <input
          type="text"
          v-model="form.quarterly_adjustment"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="quarterly_adjustment"
          id="quarterly_adjustment"
        />
      </div>
      <div>
        <label for="semiAnnual_adjustment" class="text-gray-900">Semi Annual Adjustment</label>
        <input
          type="text"
          v-model="form.semiAnnual_adjustment"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="semiAnnual_adjustment"
          id="semiAnnual_adjustment"
        />
      </div>
      <div>
        <label for="yearly_adjustment" class="text-gray-900">Yearly Adjustment</label>
        <input
          type="text"
          v-model="form.yearly_adjustment"
          class="border text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:focus:ring-blue-500 dark:focus:border-blue-500"
          name="yearly_adjustment"
          id="yearly_adjustment"
        />
      </div>
      <div>
        <label for="hourly_allowances" class="text-white">Hourly Allowances</label>
        <div class="form-check form-switch">
          <input
            type="checkbox"
            v-model="form.hourly_allowances"
            class="form-check-input appearance-none w-9 rounded-full float-left h-5 align-top bg-no-repeat bg-contain bg-gray-300 focus:outline-none cursor-pointer shadow-sm"
            role="switch"
            id="flexSwitchCheckChecked"
          />
          <label class="form-check-label inline-block text-gray-800" for="flexSwitchCheckDefault">
            True
          </label>
        </div>
      </div>
      <div>
        <label for="daily_allowances" class="text-white">Daily Allowances</label>
        <div class="form-check form-switch">
          <input
            type="checkbox"
            v-model="form.daily_allowances"
            class="form-check-input appearance-none w-9 rounded-full float-left h-5 align-top bg-no-repeat bg-contain bg-gray-300 focus:outline-none cursor-pointer shadow-sm"
            role="switch"
            id="flexSwitchCheckChecked"
          />
          <label class="form-check-label inline-block text-gray-800" for="flexSwitchCheckDefault">
            True
          </label>
        </div>
      </div>
      <div>
        <label for="monthly_allowances" class="text-white">Monthly Allowances</label>
        <div class="form-check form-switch">
          <input
            type="checkbox"
            v-model="form.monthly_allowances"
            class="form-check-input appearance-none w-9 rounded-full float-left h-5 align-top bg-no-repeat bg-contain bg-gray-300 focus:outline-none cursor-pointer shadow-sm"
            role="switch"
            id="flexSwitchCheckChecked"
          />
          <label class="form-check-label inline-block text-gray-800" for="flexSwitchCheckDefault">
            True
          </label>
        </div>
      </div>
      <div>
        <label for="quarterly_allowances" class="text-white">Quarterly Allowances</label>
        <div class="form-check form-switch">
          <input
            type="checkbox"
            v-model="form.quarterly_allowances"
            class="form-check-input appearance-none w-9 rounded-full float-left h-5 align-top bg-no-repeat bg-contain bg-gray-300 focus:outline-none cursor-pointer shadow-sm"
            role="switch"
            id="flexSwitchCheckChecked"
          />
          <label class="form-check-label inline-block text-gray-800" for="flexSwitchCheckDefault">
            True
          </label>
        </div>
      </div>
      <div>
        <label for="semiAnnual_allowances" class="text-white">Semi Annual Allowances</label>
        <div class="form-check form-switch">
          <input
            type="checkbox"
            v-model="form.semiAnnual_allowances"
            class="form-check-input appearance-none w-9 rounded-full float-left h-5 align-top bg-no-repeat bg-contain bg-gray-300 focus:outline-none cursor-pointer shadow-sm"
            role="switch"
            id="flexSwitchCheckChecked"
          />
          <label class="form-check-label inline-block text-gray-800" for="flexSwitchCheckDefault">
            True
          </label>
        </div>
      </div>
      <div>
        <label for="yearly_allowances" class="text-white">Yearly Allowances</label>
        <div class="form-check form-switch">
          <input
            type="checkbox"
            v-model="form.yearly_allowances"
            class="form-check-input appearance-none w-9 rounded-full float-left h-5 align-top bg-no-repeat bg-contain bg-gray-300 focus:outline-none cursor-pointer shadow-sm"
            role="switch"
            id="flexSwitchCheckChecked"
          />
          <label class="form-check-label inline-block text-gray-800" for="flexSwitchCheckDefault">
            True
          </label>
        </div>
      </div>
    </Modal>
  </div>
</template>
<script>
import axios from 'axios';
const apiUrl = import.meta.env.VITE_API_URL;

export default {
  data() {
    return {
      // I would like to make showPricingForm dynamiclly change and comes from another component
      showPricingForm: false,
      form: {
        room_name: '',
        room_desc: '',
        hourly_price: 0,
        daily_price: 0,
        monthly_price: 0,
        quarterly_price: 0,
        semiAnnual_price: 0,
        yearly_price: 0,
        hourly_adjusment: 0,
        daily_adjustment: 0,
        monthly_adjustment: 0,
        quarterly_adjustment: 0,
        semiAnnual_adjustment: 0,
        yearly_adjustment: 0,
        hourly_allowances: 0,
        daily_allowances: 0,
        monthly_allowances: 0,
        quarterly_allowances: 0,
        semiAnnual_allowances: 0,
        yearly_allowances: 0,
      },
    };
  },
  // show the form only if there's a circle added
  mounted() {
    window.addEventListener('show-pricing-form', (event) => {
      this.showPricingForm = event.data.showForm;
    });
  },
  methods: {
    // create room
    createRoom() {
      axios
        .post(`${apiUrl}/room`, this.form)
        .then((response) => {
          this.$message.success(`Room created successfully ${response}`);
          this.$emit('room-created');
        })
        .catch((error) => {
          console.log(error);
          this.$message.error('Error creating room');
        });
    },
  },
};
</script>
<style></style>
