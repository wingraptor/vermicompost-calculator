<template>
  <div class="calculator border p-5 rounded">
    <b-form
      @submit="onSubmit"
      @reset="onReset"
      v-if="show"
      class="d-flex flex-column align-items-center mb-5"
    >
      <!-- Width Input -->
      <b-form-group v-if="!calculatedValue" id="input-group-1" label="Width" label-for="width">
        <b-form-input
          id="width"
          type="number"
          required
          placeholder="Enter Width"
          v-model="form.width"
        ></b-form-input>
      </b-form-group>
      <!-- Height Input -->
      <b-form-group v-if="!calculatedValue" id="input-group-2" label="Height" label-for="height">
        <b-form-input
          id="height"
          type="number"
          required
          placeholder="Enter Height"
          v-model="form.height"
        ></b-form-input>
      </b-form-group>
      <!-- Units Input -->
      <b-form-group  v-if="!calculatedValue" id="units" label="Units">
        <b-form-radio-group id="radio-group" v-model="form.units" required>
          <b-form-radio value="feet">Feet</b-form-radio>
          <b-form-radio value="meters">Meters</b-form-radio>
        </b-form-radio-group>
      </b-form-group>

      <!-- <b-form-group id="input-group-3" label="Food:" label-for="input-3">
        <b-form-select id="input-3" required></b-form-select>
      </b-form-group> -->
      <div class="buttons d-flex justify-content-around w-100">
        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </div>
    </b-form>
    <!-- Results Div -->
    <div v-if="calculatedValue" class="results d-flex flex-column align-items-center">
      <h1>You Need:</h1>
      <h5><span class="text-danger">{{ (calculatedValue).toFixed(2) }}</span> lbs  of vermicompost</h5>
      <h5 class=text-center>OR</h5>
      <h5><span class="text-danger">{{ (calculatedValue / 2.2).toFixed(2) }}</span> kg  of vermicompost</h5>
      <h5 class=text-center>OR</h5>
      <h5><span class="text-danger">{{ ( calculatedValue / 4.5).toFixed(1) }}</span> x 4.5 lbs bags of vermicompost</h5>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  props: {},
  data() {
    return {
      selected: "feet",
      constants: {
        vermicompostMassPerM2: 1.0764,
        vermicompostMassPerSqFt: 0.1,
      },
      form: {
        width: "",
        height: "",
        units: "",
      },
      show: true,
      calculatedValue: "",
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      this.calculateVermicompostMass(this.form);
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.width = "";
      this.form.height = "";
      this.form.units = "";

      // Reset calculated value
      this.calculatedValue = "";

      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
    calculateVermicompostMass(formData) {
      const { width, height, units } = formData;
      const area = width * height;
      let multiplier;
      units === "meters"
        ? (multiplier = this.constants.vermicompostMassPerM2)
        : (multiplier = this.constants.vermicompostMassPerSqFt);

      this.calculatedValue = area * multiplier;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
