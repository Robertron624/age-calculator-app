# Frontend Mentor - Age calculator app solution

This is a solution to the [Age calculator app challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/age-calculator-app-dF9DFFpj-Q). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

Users should be able to:

- View an age in years, months, and days after submitting a valid date through the form
- Receive validation errors if:
  - Any field is empty when the form is submitted
  - The day number is not between 1-31
  - The month number is not between 1-12
  - The year is in the future
  - The date is invalid e.g. 31/04/1991 (there are 30 days in April)
- View the optimal layout for the interface depending on their device's screen size
- See hover and focus states for all interactive elements on the page
- **Bonus**: See the age numbers animate to their final number when the form is submitted

### Screenshot

![](./screenshot.jpg)

### Links

- Solution URL: [Solution URL](https://github.com/Robertron624/age-calculator-app)
- Live Site URL: [Live site URL](https://your-live-site-url.com)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- Mobile-first workflow
- [Vue](https://vuejs.org/) - JS library
- [Vite](https://vitejs.dev/) - Build tool

### What I learned

This was my first ever vue project and I learned a lot. I learned how to use vue and how to create a form in vue, how to bind the inputs
to the data and how to handle the form. I also learned how to use the vue cli, conditional rendering and conditional classes to change
the input colors to red when there are errors with the submitted date.

Some code I am proud of:

Each input with his label and error message.
```html
<div class="input-container">
  <label :class="{'error-label': inputErrors.daysErrors || dateError}" for="day">Day</label>
  <input
    :class="{'error-border': inputErrors.daysErrors || dateError}"
    v-model="daysInput"
    placeholder="DD"
    type="number"
    name="day"
    id="day"
  />
  <span v-if="inputErrors.daysErrors" class="error-msg">{{ inputErrors.daysErrors }}</span>
</div>
```

The function that handles the form submission and validation.
```js
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
```

### Continued development

I want to keep using vue and learn more about it. I want to learn how to use vue router and pinia for managing global state. My main
framework will still be react for intermediate and advance projects but I want to begin using vue for newbie and junior projects.

### Useful resources

- [How to create a form in Vue.js](https://www.educative.io/answers/how-to-create-a-form-in-vuejs) - This helped me to create a form in vue and how to handle it.
- [Get Year, Month and Day from a Date Object in JavaScript](https://bobbyhadz.com/blog/javascript-get-year-month-day-from-date) - This is an amazing article which helped me understand cuando to get the year, month and day from a date object in javascript to validate.
- [Class and Style binding](https://vuejs.org/guide/essentials/class-and-style.html) how to use conditional classes in vue.
- [Getting started with Vue](https://vuejs.org/guide/introduction.html)

## Author

- Personal Website - [Robert Ramirez](https://robert-ramirez.netlify.app)
- Frontend Mentor User- [@Robertron624](https://www.frontendmentor.io/profile/Robertron624)
- Twitter - [@robertdowny](https://www.twitter.com/robertdowny)

## Acknowledgments

- [Borislav Hadzhiev](https://bobbyhadz.com/) his article I mentioned in useful resources.
