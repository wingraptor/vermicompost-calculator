<template>
  <div class="calculator">
    <b-form @submit="onSubmit">
      <b-form-group id="units" label="Units">
        <b-form-radio-group id="radio-group" v-model="form.units">
          <b-form-radio value="feet">Feet</b-form-radio>
          <b-form-radio value="meters">Meters</b-form-radio>
        </b-form-radio-group>
      </b-form-group>

      <b-form-group id="input-group-1" label="Width" label-for="width">
        <b-form-input
          id="width"
          type="number"
          required
          placeholder="Enter Width"
          v-model="form.width"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Height" label-for="height">
        <b-form-input
          id="height"
          type="number"
          required
          placeholder="Enter Height"
          v-model="form.height"
        ></b-form-input>
      </b-form-group>

      <!-- <b-form-group id="input-group-3" label="Food:" label-for="input-3">
        <b-form-select id="input-3" required></b-form-select>
      </b-form-group> -->

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <div class="results">
      <h1>You Need</h1>
      <span>{{ calculatedValue }} kg </span>
      <span>of vermicompost</span>
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
      calculatedValue: "",
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      this.calculateVermicompostMass(this.form);
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
