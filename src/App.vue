<script>
  export default {
    data() {
      return {
        years: "--",
        months: "--",
        days: "--",
        yearsInput: "",
        monthsInput: "",
        daysInput: "",
      }
    },
    methods: {
      calculate() {
        console.log("submitted !!")
        const date = new Date(this.yearsInput, this.monthsInput, this.daysInput);
        const today = new Date();

        const diff = today - date;
        const diffInYears = (diff / (1000 * 60 * 60 * 24)) / 365;
        const diffInMonths =  Math.abs(today.getMonth() +1 - date.getMonth());
        const diffInDays = Math.abs(today.getUTCDate() - date.getUTCDate());
        this.years = Math.floor(diffInYears);
        this.months = Math.floor(diffInMonths);
        this.days = Math.floor(diffInDays);
      },
    },
  }

</script>

<template>

  <main>
    <div class="container">
      <div class="date-inputs">
        <form action="GET" @submit.prevent="calculate">
          <div class="input-container">
              <label for="day">Day</label>
              <input v-model="daysInput" placeholder="DD" type="number" name="day" id="day">
          </div>
          <div class="input-container">
              <label for="month">Month</label>
              <input v-model="monthsInput" placeholder="MM" type="number" name="month" id="month">
          </div>
          <div class="input-container">
            <label for="year">year</label>
            <input v-model="yearsInput" placeholder="YYYY" type="number" name="year" id="year">
          </div>
          <button role="button" class="arrow" type="submit">
          <svg xmlns="http://www.w3.org/2000/svg" width="46" height="44" viewBox="0 0 46 44"><g fill="none" stroke="#FFF" stroke-width="2"><path d="M1 22.019C8.333 21.686 23 25.616 23 44M23 44V0M45 22.019C37.667 21.686 23 25.616 23 44"/></g></svg>
        </button>
        </form>
        <!-- <img class="arrow" src="icon-arrow.svg" alt="arrow"> -->

      </div>
      <div class="calculation">
        <span>{{ years }} <strong>years</strong></span>
        <span>{{ months }} <strong>months</strong></span>
        <span>{{ days }} <strong>days</strong></span>
      </div>
    </div>
  </main>
</template>

<style scoped>

main {
  --off-white: hsl(0, 0%, 94%);
  --light-grey: hsl(0, 0%, 86%);
  --smokey-grey: hsl(0, 1%, 44%);
  --purple: hsl(259, 100%, 65%);

}

.container {
  max-width: 90%;
  margin: 0 auto;
  padding: 0 2rem;
  background-color: white;
  border-radius: 20px 20px 26% 20px;
}


.date-inputs {
  padding: 2rem 0 3rem 0;
  border-bottom: 1px solid var(--light-grey);
  position: relative;
}

.arrow {
  border-color: transparent;
  position: absolute;
  bottom: -155%;
  right: 39%;
  transform: translateY(-50%);
  background-color: var(--purple);
  border-radius: 50%;
  width: 40px;
  padding: .4rem;
  transition: all .3s ease-in-out;
  cursor: pointer;
}

.arrow svg {
  display: block;
  width: 25px;
  height: 25px;
}

.arrow:hover {
  background-color: black;
}


.date-inputs form{
    display: flex;
    justify-content: space-between;
}

.date-inputs .input-container {
  display: flex;
  flex-direction: column;
}

.date-inputs label {
  font-size: 0.7rem;
  font-weight: 600;
  color: var(--smokey-grey);
  text-transform: uppercase;
}

.date-inputs input {
  width: 4rem;
  height: 2.4rem;
  font-size: 1rem;
  font-weight: 600;
  border: 1px solid var(--light-grey);
  outline: none;
  border-radius: 5px;
  padding-left: .5rem;
}

.date-inputs input:focus {
  border: 1px solid var(--purple);
}

.calculation {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 3rem 0;
  line-height: 50px;
}

.calculation span {
  font-size: 3rem;
  font-weight: 800;
  color: var(--purple);
  font-style: italic;
  width: 100%;
}
.calculation span strong {
  color: black;
  font-weight: 800;
}

@media (min-width: 768px) {
  .container {
    max-width: none;
    min-width: 450px;
  }

  .arrow {
    right: -25%;
  }

  .date-inputs input {
    width: 5rem;
  }

  .date-inputs form {
    width: 70%;
  }
}
</style>
