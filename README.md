# Currency Converter

## **Overview**
This is a responsive **Currency Converter** application built using HTML, CSS, and JavaScript. Users can input an amount, select a source and target currency, and get real-time exchange rates. The application uses a public currency API to fetch the latest rates.

---

## **Features**
- Real-time currency conversion using the latest exchange rates.
- Dropdown menus with country flags for selecting currencies.
- Validation for input amounts.
- User-friendly interface with clear messages for conversions.
- Mobile-friendly and responsive design.

---

## **Technologies Used**
- **HTML**: Provides the structure for the application.
- **CSS**: Styles the application and ensures a responsive design.
- **JavaScript**: Implements the logic for fetching data and performing conversions.
- **Currency API**: Fetches the latest exchange rates.

---

## **How to Use**
1. Enter the amount you wish to convert in the input field.
2. Select the source currency from the "From" dropdown menu.
3. Select the target currency from the "To" dropdown menu.
4. Click the **Get Exchange Rate** button.
5. View the converted amount and the exchange rate in the message box.

---

## **File Structure**
- `index.html`: Contains the HTML structure of the application.
- `style.css`: Handles the styling and layout of the app.
- `app.js`: Implements the core logic for currency conversion.
- `codes.js`: Contains the country codes and their corresponding currency codes.

---

## **Code Explanation**

### **1. HTML Structure**
The `index.html` file defines the layout, including input fields, dropdowns for currency selection, and a button for fetching the exchange rate.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Currency Converter</title>
    <link href="style.css" rel="stylesheet" />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div class="container">
      <h2>Currency Converter</h2>
      <form>
        <div class="amount">
          <p>Enter Amount</p>
          <input value="1" type="text" />
        </div>
        <div class="dropdown">
          <div class="from">
            <p>From</p>
            <div class="select-container">
              <img src="https://flagsapi.com/US/flat/64.png" />
              <select name="from"></select>
            </div>
          </div>
          <i class="fa-solid fa-arrow-right-arrow-left"></i>
          <div class="to">
            <p>To</p>
            <div class="select-container">
              <img src="https://flagsapi.com/IN/flat/64.png" />
              <select name="to"></select>
            </div>
          </div>
        </div>
        <div class="msg">1USD = 80INR</div>
        <button>Get Exchange Rate</button>
      </form>
    </div>
    <script src="codes.js"></script>
    <script src="app.js"></script>
  </body>
</html>
```

---

### **2. CSS Styling**
The `style.css` file ensures a clean and responsive design with modern aesthetics.

```css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f4e4ba;
}

.container {
  background-color: #fff;
  padding: 2rem;
  border-radius: 1rem;
  min-height: 45vh;
  width: 40vh;
}

form {
  margin: 2rem 0;
}

form input {
  width: 100%;
  border: 1px solid lightgray;
  font-size: 1rem;
  height: 3rem;
  padding-left: 0.5rem;
  border-radius: 0.75rem;
}

.dropdown {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 2rem;
}

.select-container {
  display: flex;
  align-items: center;
  border: 1px solid lightgray;
  border-radius: 0.5rem;
}

form button {
  height: 3rem;
  background-color: #af4d98;
  color: #fff;
  font-size: 1.15rem;
  cursor: pointer;
}
```

---

### **3. JavaScript Logic**
The `app.js` file fetches the latest exchange rates and calculates conversions.

```javascript
const BASE_URL = "https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies";
const dropdowns = document.querySelectorAll(".dropdown select");
const btn = document.querySelector("form button");
const fromCurr = document.querySelector(".from select");
const toCurr = document.querySelector(".to select");
const msg = document.querySelector(".msg");

for (let select of dropdowns) {
  for (currCode in countryList) {
    let newOption = document.createElement("option");
    newOption.innerText = currCode;
    newOption.value = currCode;
    if (select.name === "from" && currCode === "USD") {
      newOption.selected = "selected";
    } else if (select.name === "to" && currCode === "INR") {
      newOption.selected = "selected";
    }
    select.append(newOption);
  }
  select.addEventListener("change", (evt) => {
    updateFlag(evt.target);
  });
}

const updateExchangeRate = async () => {
  let amount = document.querySelector(".amount input");
  let amtVal = amount.value;
  if (amtVal === "" || amtVal < 1) {
    amtVal = 1;
    amount.value = "1";
  }
  const URL = `${BASE_URL}/${fromCurr.value.toLowerCase()}/${toCurr.value.toLowerCase()}.json`;
  let response = await fetch(URL);
  let data = await response.json();
  let rate = data[toCurr.value.toLowerCase()];

  let finalAmount = amtVal * rate;
  msg.innerText = `${amtVal} ${fromCurr.value} = ${finalAmount} ${toCurr.value}`;
};

btn.addEventListener("click", (evt) => {
  evt.preventDefault();
  updateExchangeRate();
});

window.addEventListener("load", () => {
  updateExchangeRate();
});
```

---

## **Screenshots**
- **Initial Screen**: Default selection of USD to INR with a placeholder amount.
- **Conversion Result**: Displays the calculated conversion and exchange rate.

---

## **How to Run the Application**
1. Clone the repository or download the files.
2. Open the `index.html` file in any modern web browser.
3. Use the application to convert currencies in real-time.

---

## **API Used**
- The application uses the free [Currency API](https://github.com/fawazahmed0/currency-api) hosted on jsDelivr for fetching exchange rates.

---

## **Future Enhancements**
- Add support for historical exchange rates.
- Implement a feature for swapping the "From" and "To" currencies.
- Provide a graph for currency trends.
