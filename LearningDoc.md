# Learning Doc


- [Learning Doc](#learning-doc)
- [Week 4](#week-4)
  - [July 19th, 2021](#july-19th-2021)
    - [React](#react)
      - [Cypress Test](#cypress-test)
      - [React Test](#react-test)
- [Week 3](#week-3)
  - [July 12th, 2021](#july-12th-2021)
    - [Bank Challenge](#bank-challenge)
    - [Thermostat](#thermostat)
  - [July 13th, 2021](#july-13th-2021)
    - [Cypress](#cypress)
    - [Thermostat Visual](#thermostat-visual)
  - [July 14th, 2021](#july-14th-2021)
    - [JQuery](#jquery)
    - [Async Programming](#async-programming)
  - [July 15, 2021](#july-15-2021)
    - [Ajax](#ajax)
    - [Process observations](#process-observations)
- [Week 2](#week-2)
  - [July 6th, 2021](#july-6th-2021)
    - [Refactor Bob's Bagel Green](#refactor-bobs-bagel-green)
  - [July 7th, 2021](#july-7th-2021)
    - [Bob's Bagels Red](#bobs-bagels-red)
  - [July 8th 2021](#july-8th-2021)
    - [Coupling Part 2](#coupling-part-2)
  - [July 9th, 2021](#july-9th-2021)
    - [Twilio](#twilio)
- [Week 1](#week-1)
  - [July 2nd, 2021](#july-2nd-2021)
    - [Coupling](#coupling)
  - [July 4th, 2021](#july-4th-2021)
    - [Airport Challenge](#airport-challenge)

# Week 4

## July 19th, 2021

### React
I started by creating my first app using the react framework. This was fairly simple and only involved creating a project and changing around some of the html elements.

```js
import './App.css';

function App() {
  return (
    <p id = "greeting">hello world</p>
  );
}

export default App;
```
![Screenshot of react Hello world](images/Week4/ReactHelloWorld.png)

This process involved writing cypress tests and react tests.

#### Cypress Test

```js
it('App test', () => {
    cy.visit('/');
    cy.get('#greeting').should("contain", "hello world");
})
```
![Screenshot of passing cypress tests](images/Week4/ReactHelloWorld.png)

#### React Test

```js
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/Hello World/i);
  expect(linkElement).toBeInTheDocument();
});
```
![The first react test passing](images/Week4/ReactFirstTestPass.png)

# Week 3

## July 12th, 2021

### Bank Challenge
I gave and recieved feedback for the bank challenge. I thought I did well overall, but others had interesting ideas on how to make the code neater and easier to read.

### Thermostat
We wrote a thermostat class in a pair. This involved in depth pair programming.
https://github.com/RyanVanDijck/Thermostat/commits/master

## July 13th, 2021

### Cypress
I started by learning the basics on how to write tests and run tests using the Cypress framework.

This framework allows you to write tests that look at the contents of a webpage.

I changed code to pass prewritten tests.

### Thermostat Visual
I was able to convert the thermostat class into a visual webpage.

https://user-images.githubusercontent.com/71043499/125642602-d760f281-c10d-4888-8492-fac809a99ff7.mp4


## July 14th, 2021

### JQuery

I was able to learn the basics of JQuery, and use it to simplify the source code of the thermostat.

```js
$( document ).ready(function() {
  const thermostat = new Thermostat();

  $("#power").text(thermostat.onPowerSaving());

  $( "#down" ).click(function( event ) {
    $( "#message" ).text(thermostat.down());
    $("#usage").text(thermostat.getUsage());
  });

  $("#button").click((event) => {
    $( "#message" ).text(thermostat.up());
    $("#usage").text(thermostat.getUsage());
  })
  $("#change").click((event) => {
    thermostat.changePowerSaving();
    $("#power").text(thermostat.onPowerSaving());

  })
  $("#reset").click((event) => {
    $("#message").text(thermostat.reset);
    $("#usage").text(thermostat.getUsage());
  })
});
```
### Async Programming

Afterwards, I completed work based on Async programming with a pair partner. The purpose of the exercise was to run code that involved functions that need to wait for something. We needed to predict in what order different lines of code would run.

```js
console.log(1)
$(document).click(function(clickEvent) {
    console.log(3)
    console.log("The click event:", clickEvent);
    console.log(4)
});
console.log(2)
```

```js
console.log(1)
setTimeout(function hiThere(){
    console.log("Hi there!");
  console.log(3)
  console.log(4)
  },0)
console.log(2);
```

## July 15, 2021
### Ajax
We started by trying to add an api to the thermostat.

```js
function getTemp(){
  return $.get(`http://api.openweathermap.org/data/2.5/weather?q=London&appid=${appid}`, (response) => {
    console.log(response.main.temp);
    return (response.main.temp - 273.15).toFixed(0);
  });
}

$( document ).ready(function() {
  const temp = setTimeout(() => {
    return getTemp();
  }, 0);
```

This involved using a weather api to acces the current temperature. There was a minor error.

### Process observations
I needed to do a process observation today. It mainly went well, but I had some difficulties with eslint and vscode.

I could improve by thinking about and writing tests about the core functionality before thinking about the state of the program.

# Week 2
## July 6th, 2021
### Refactor Bob's Bagel Green

Refactored Bob's Bagel Green based on things noticed on the 6th

![pairprogramming](images/Week2/Pair%20Programming.png)

## July 7th, 2021
### Bob's Bagels Red
Started work on Bob's Bagels Red edition. Managed to create a domain model.
Object|Properties|Messages|Context|Output
---|---|---|---|---
Basket|max_capacity @Number|Order|Basket Not Full and Item exists|@Array[@String]
||basket @array[@String]||Basket is full|@Error[@String 'Basket is full']
||cost @Cost||Item not found|@String
||receipt @reciept|Remove|Exists In Basket|@Array[@String]
||||Does not exist in basket|@Error[@String "Was never in your basket."]
|Receipt|totalPrices @Number|quantity|Basket Object|@String
|||getPrice|Item and number of that Item given|@Number
Cost|total @Number|total|Basket Given|@String
|||howMany|Basket and item given|@Number

## July 8th 2021
### Coupling Part 2
Did more work on coupling.

This involved changing:

```js
items = [
      new Item(1),
      new Item(2),
      new Item(3),
    ];
```


into:

```js
items = [
      {price: 1},
      {price: 2},
      {price: 2},
    ];
```
This is so that the testing in this class is not dependent on the item class. This means that if the item class changes or is broken, this does not affect the testing of this class.

I also replaced this:
```js
printReceipt () {
    const receipt = new Receipt(this.total());
    return receipt.print();
}
```

with this:
```js
printReceipt (ReceiptPointer = Receipt) {
    const receipt = new ReceiptPointer(this.total());
    return receipt.print();
}
```
This is so that you can provide an alternative of the receipt class in the method, which means that the class has become more decoupled.  

## July 9th, 2021
### Twilio
I used the twilio service and npm library to send a text message to my phone.

```js
client.messages
  .create({
     body: 'This is my test message',
     from: '**********',
     to: '**********'
   })
  .then(message => console.log(message.sid));
```
![Recieved Message from Twilio](images/Week2/twilio.jpg)

# Week 1
## July 2nd, 2021
### Coupling

Successfully completed task on Coupling.
https://github.com/RyanVanDijck/Coupling


## July 4th, 2021
### Airport Challenge
Completed the airport challenge. This involved writing tests before hand and writing code against those tests.

https://github.com/RyanVanDijck/airport-challenge
