<template>
  <div class="calculator border p-4 rounded bg-light shadow-lg mb-4">
    <!-- Calculation Form -->
    <b-form
      @submit="onSubmit"
      @reset="onReset"
      v-if="show && !calculatedValue"
      class="d-flex flex-column align-items-center"
    >

    <h2>Calculator</h2>

      <!-- Width Input -->
      <b-form-group id="input-group-1" label="Width of bed" label-for="width">
        <b-form-input
          id="width"
          type="number"
          required
          placeholder="Enter Width"
          v-model="form.width"
        ></b-form-input>
      </b-form-group>

      <!-- length Input -->
      <b-form-group id="input-group-2" label="Length of bed " label-for="length">
        <b-form-input
          id="length"
          type="number"
          required
          placeholder="Enter Length"
          v-model="form.length"
        ></b-form-input>
      </b-form-group>

      <!-- Units Input -->
      <b-form-group id="units" label="Units">
        <b-form-radio-group id="radio-group" v-model="form.units" required>
          <b-form-radio value="feet">Feet</b-form-radio>
          <b-form-radio value="meters">Meters</b-form-radio>
        </b-form-radio-group>
      </b-form-group>
      
      <!-- Form Buttons -->
      <div class="buttons d-flex justify-content-around w-100">
        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </div>
    </b-form>

    <!-- Results Display Div -->
    <div v-if="calculatedValue" class="results d-flex flex-column align-items-center text-center">
      <h1 class="mb-3">You Need:</h1>
      <h5><span class="text-danger">{{ (calculatedValue).toFixed(2) }}</span> lbs  of vermicompost</h5>
      <h5 class=text-center>or</h5>
      <h5><span class="text-danger">{{ (calculatedValue / 2.2).toFixed(2) }}</span> kg  of vermicompost</h5>
      <h5 class=text-center>or</h5>
      <h5><span class="text-danger">{{ calculatedValue | calculatedNumberOfBags }}</span> x 4.5 lbs bags of vermicompost</h5>
      <b-button type="reset" variant="danger" @click=" calculatedValue = ''">Reset</b-button>
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
        length: "",
        units: "",
      },
      show: true,
      // Presence of absence of calculatedValue controls whether results div or form div are displayed
      calculatedValue: "",
    };
  },
  methods: {
    // Handle submission of form
    onSubmit(evt) {
      evt.preventDefault();
      this.calculateVermicompostMass(this.form);
    },
    // Handle Reset of Form
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.width = "";
      this.form.length = "";
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
      const { width, length, units } = formData;
      const area = width * length;
      let multiplier;
      units === "meters"
        ? (multiplier = this.constants.vermicompostMassPerM2)
        : (multiplier = this.constants.vermicompostMassPerSqFt);

      this.calculatedValue = area * multiplier;
    },
  },
  filters :{ 
    calculatedNumberOfBags(calculatedValue){
        return calculatedValue < 4.5 ? 1 : Math.ceil(( calculatedValue / 4.5).toFixed(1)) 
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 60%;
}
</style>
