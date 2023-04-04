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
        inputErrors : {
          yearsErrors: "",
          monthsErrors: "",
          daysErrors: "",
        },
        dateError: false,
      }
    },
    methods: {

      checkEmpty() {

        let empties = 0;

        const EMPTYMSG = "This field is required";

        if (this.yearsInput === "") {
          this.inputErrors.yearsErrors = EMPTYMSG;
          empties++;
        } else {
          this.inputErrors.yearsErrors = "";
        }
        if (this.monthsInput === "") {
          this.inputErrors.monthsErrors =  EMPTYMSG;
          empties++;
        } else {
          this.inputErrors.monthsErrors = "";
        }
        if (this.daysInput === "") {
          this.inputErrors.daysErrors =  EMPTYMSG;
          empties++;
        } else {
          this.inputErrors.daysErrors = "";
        }

        return empties
      },

      isNumberValid (type, value) {
        const INVALIDMSG = "Must be a valid ";
        const currentYear = new Date().getFullYear();
        let isValid = true;
        switch(type) {
          case "day":
            if (value > 31 || value < 1) {
              console.log("if day")
              isValid = false;
              this.inputErrors.daysErrors = INVALIDMSG + type;
            } else {
              this.inputErrors.daysErrors = "";
            }
            break;
          case "month":
            if (value > 12 || value < 1) {
              console.log("if month")
              this.inputErrors.monthsErrors = INVALIDMSG + type;
              isValid = false;
            } else {
              this.inputErrors.monthsErrors = "";
            }
            break;
          case "year":
            if (value > currentYear) {
              console.log("if year")
              this.inputErrors.yearsErrors = INVALIDMSG + type;
              isValid = false;
            } else {
              this.inputErrors.yearsErrors = "";
            }
            break;
        }
        return isValid;
      },
      
      isDateValid (year, month, day) {
        const date = new Date(year, month-1, day); // month is 0 based, thats why we need to subtract 1 from the users input

        // check if year, month and day are the same ( we stract 1 from the users input because in date object a month is 0 based )
        if (date.getFullYear() == year && date.getMonth() == month - 1 && date.getDate() == day) {
          return true;
        } else {
          return false;
        }
      },
      
      calculate() {

        if(this.checkEmpty() > 0) return;

        const validDay = this.isNumberValid("day", this.daysInput);
        const validMonth = this.isNumberValid("month", this.monthsInput);
        const validYear = this.isNumberValid("year", this.yearsInput);

        if (!validDay || !validMonth || !validYear) return;

        if(!this.isDateValid(this.yearsInput, this.monthsInput, this.daysInput)) {
          this.dateError = true;
          return;
        }else {
          this.dateError = false;
        }


        const date = new Date(this.yearsInput, this.monthsInput, this.daysInput);
        const today = new Date();

        const diff = today - date;
        const diffInYears = (diff / (1000 * 60 * 60 * 24)) / 365;
        const diffInMonths =  Math.abs(today.getMonth() + date.getMonth());
        const diffInDays = Math.abs(today.getUTCDate() - date.getUTCDate());
        this.years = Math.floor(diffInYears);
        this.months = Math.floor(diffInMonths);
        this.days = 31 - Math.floor(diffInDays);
        console.log("submitted !!")
      },
    },
  }

</script>

<template>

  <main>
    <div class="container">
      <div class="date-inputs">
        <form action="GET" @submit.prevent="calculate">
          <div class="inputs">
            <div class="input-container">
                <label :class="{'error-label': inputErrors.daysErrors || dateError}" for="day">Day</label>
                <input :class="{'error-border': inputErrors.daysErrors || dateError}" v-model="daysInput" placeholder="DD" type="number" name="day" id="day">
                <span v-if="inputErrors.daysErrors" class="error-msg">{{ inputErrors.daysErrors }}</span>
            </div>
            <div class="input-container">
                <label :class="{'error-label': inputErrors.monthsErrors || dateError}" for="month">Month</label>
                <input :class="{'error-border': inputErrors.monthsErrors || dateError}" v-model="monthsInput" placeholder="MM" type="number" name="month" id="month">
                <span v-if="inputErrors.monthsErrors" class="error-msg">{{ inputErrors.monthsErrors }}</span>
            </div>
            <div class="input-container">
              <label :class="{'error-label': inputErrors.yearsErrors || dateError}" for="year">year</label>
              <input :class="{'error-border': inputErrors.yearsErrors || dateError}" v-model="yearsInput" placeholder="YYYY" type="number" name="year" id="year">
              <span v-if="inputErrors.yearsErrors" class="error-msg">{{ inputErrors.yearsErrors }}</span>
            </div>
          </div>
          <div class="button-container">
            <button role="button" class="arrow" type="submit">
            <svg xmlns="http://www.w3.org/2000/svg" width="46" height="44" viewBox="0 0 46 44"><g fill="none" stroke="#FFF" stroke-width="2"><path d="M1 22.019C8.333 21.686 23 25.616 23 44M23 44V0M45 22.019C37.667 21.686 23 25.616 23 44"/></g></svg>
            </button>
          </div>
        </form>
        <!-- <img class="arrow" src="icon-arrow.svg" alt="arrow"> -->
        <span v-if="dateError" class="error-msg">Must be a valid date</span>
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
  --light-red: hsl(0, 100%, 67%);

}

.container {
  max-width: 90%;
  margin: 0 auto;
  padding: 0 2rem;
  background-color: white;
  border-radius: 20px 20px 26% 20px;
}

.date-inputs {
  padding: 2rem 0 0rem 0;
  /* border-bottom: 1px solid var(--light-grey); */
  position: relative;
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 3.5rem;
  position: relative;
  border-bottom: 1px solid var(--light-grey);
}

.arrow {
  border-color: transparent;
  position: absolute;
  width: 58px;
  background-color: var(--purple);
  border-radius: 50%;
  padding: .8rem;
  transition: all .3s ease-in-out;
  cursor: pointer;
  align-self: center;
}

.arrow::after {
  content: "";
  height: 2px;
  width: 100%;
  background-color: var(--purple);
}

.arrow svg {
  display: block;
  width: 100%;
  height: 25px;
}

.arrow:hover {
  background-color: black;
}

.date-inputs form{
    display: flex;
    justify-content: space-between;
    flex-direction: column;
}

.date-inputs .inputs {
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
  width: 5rem;
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

.error-msg {
  color: var(--light-red);
  font-size: 0.5rem;
  margin-top: .3rem;
  font-weight: 300;
  text-transform: capitalize;
  font-style: italic;
}

.error-border {
  border: 1px solid var(--light-red) !important;
}

.error-label {
  color: var(--light-red) !important;
}

@media (min-width: 768px) {
  .container {
    max-width: none;
    min-width: 450px;
  }

  .arrow {
    right: 0%;
  }

  .date-inputs form {
    width: 100%;
  }

  .date-inputs .inputs {
    width: 80%;
  }

  .button-container {
    margin-top: 1.5rem;
  }

  .calculation {
    padding-top: 2rem;
  }

}
</style>
