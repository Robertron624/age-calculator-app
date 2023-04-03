<script setup>

</script>

<template>

  <main>
    <div class="container">
      <div class="date-inputs">
        <form action="GET">
          <div class="input-container">
              <label for="day">Day</label>
              <input placeholder="DD" type="number" name="day" id="day">
          </div>
          <div class="input-container">
              <label for="month">Month</label>
              <input placeholder="MM" type="number" name="month" id="month">
          </div>
          <div class="input-container">
            <label for="year">year</label>
            <input placeholder="YYYY" type="number" name="year" id="year">
          </div>
        </form>
        <img class="arrow" src="icon-arrow.svg" alt="arrow">
      </div>
      <div class="calculation">
        <span>38 <strong>years</strong></span>
        <span>3 <strong>months</strong></span>
        <span>26 <strong>days</strong></span>
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
  padding: 0 1rem;
  background-color: white;
  border-radius: 20px 20px 26% 20px;
}


.date-inputs {
  padding: 2rem 0 3rem 0;
  border-bottom: 1px solid var(--light-grey);
  position: relative;
}

.arrow {
  position: absolute;
  top: 100%;
  right: 39%;
  transform: translateY(-50%);
  background-color: var(--purple);
  border-radius: 50%;
  width: 40px;
  padding: .4rem;
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
    right: 7%;
  }
}
</style>
