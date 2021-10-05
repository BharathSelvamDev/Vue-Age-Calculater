<template>
  <div class="age">
    <v-card elevation = "10"  class="dp-card" max-width="500">
      <div class="inner-c">
        <div class="c-1">
          <v-date-picker
            class="picker"
            v-model="dob"
            elevation="15"
            color="green lighten-1"
            header-color="success"
            :max="todayDate"
          ></v-date-picker>
        </div>
        <div class="c-2">
          <v-btn @click="CalculateAge()" color="primary">Get My Age</v-btn>
        </div>
      </div>
    </v-card>

    <div v-if="ageInYears != null" class="details">
      <v-card elevation = "10" class="de-card" max-width="500" color="#cecece">
        <pre>Date Of Birth  : {{ dob }}</pre>
        <pre>Age in Years   : {{ ageInYears }} Years</pre>
        <pre  v-if="ageInYears > 1 ">Age in Months  : {{ ageInMonths }} Months</pre>
        <pre  v-if="ageInYears > 1 " >Age in Weeks   : {{ ageInWeeks }} Weeks</pre>
        <pre  v-if="ageInYears > 1 " >Age in Days    : {{ ageInDays }} Days</pre>
        <pre  v-if="ageInYears > 1 " >Age in Hours   : {{ ageInHours }} Hours</pre>
        <pre  v-if="ageInYears > 1 " >Age in Minutes : {{ ageInMinutes }} Minutes</pre>
        <pre  v-if="ageInYears > 1 " >Age in Seconds : {{ ageInSeconds }} Seconds</pre>
      </v-card>
    </div>
  </div>
</template>

<script>
export default {
  name: "AgeComponent",
  data() {
    return {
      dob: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
      todayDate: "",
      ageInYears: null,
      ageInMonths: null,
      ageInWeeks : null,
      ageInDays: null,
      ageInHours: null,
      ageInMinutes: null,
      ageInSeconds: null,
    };
  },
  mounted() {
    var today = new Date();
    var dd = String(today.getDate()).padStart(2, "0");
    var mm = String(today.getMonth() + 1).padStart(2, "0");
    var yyyy = today.getFullYear();
    today = yyyy + "-" + mm + "-" + dd;
    this.todayDate = today;
  },
  methods: {
    CalculateAge() {
      var birthDate = new Date(this.dob);
      var otherDate = new Date(this.todayDate);

      console.log(birthDate);
      console.log(otherDate);

      var years = otherDate.getFullYear() - birthDate.getFullYear();

      console.log(years);

      if (
        otherDate.getMonth() < birthDate.getMonth() ||
        (otherDate.getMonth() == birthDate.getMonth() &&
          otherDate.getDate() < birthDate.getDate())
      ) {
        years--;
      }
      this.ageInYears = years;
      this.ageInMonths = years * 12 ;
      this.ageInWeeks =  years * 52 ;
      this.ageInDays =  years * 365 ;
      this.ageInHours =  years * 8760 ;
      this.ageInMinutes = years * 525600 ;
      this.ageInSeconds  = years * 31536000 ;
    },
  },
};
</script>

<style scoped>
.age {
  margin: 50px;
  display: flex;
}

.dp-card {
  padding: 10px;
}

.details {
  width: 50%;
  margin: 0 auto;
  margin-left: 20px;
  font-weight: bolder   ;
}

.de-card {
  padding : 3%;
  height: auto;
  color: black;
}

.picker {
  margin: 30px;
}

.inner-c {
  display: flex;
}

.c-2 {
  margin-top: 200px;
}
</style>
