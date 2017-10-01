# Vue-todos

Simple todo-app to showcase basic functionality of vuejs

## Vue survival tutorial

### The new frontend VIEW frameworks (Optional read)

On recent years, we´ve been experiencing the birth of several frontend applications that aim to solve several problems in web app development on their own ways. Some notorious examples:

- AngularJS
- ReactJS
- Handlebars

Those frameworks were so successful at solving most of the frontend problems that they settled a new whole way of developing web applications on the frontend, one that is highly efficient, fast, robust and scalable.

If you've been a web developer for a while, you must be already familiar with modifying the DOM with both raw Javascript  and Jquery.

While this classic approach of modifying the DOM with javascript or Jquery is pretty simple, it comes with a high development time overhead and most of the time with unexpected bugs and behaviours due to the need of controlling all the modifications to the dom and all of the possible common mistakes that comes with it, it also generates code that doesn't scale most of the time.

Frameworks like the classic AngularJS, or ReactJS settled a new way of interacting with dynamic data and binding it to the dom without the need of huge methods and scripts in order to add an element fetched from a server to an unordered list for example.

In this case, VueJS takes lots of highly successful concepts from those frameworks and takes a step further by being highly adaptable, fast, and having a very friendly learning curve.

### Data binding

One of those succesful concepts is data binding. Data binding was born with the need of having a managed DOM in order to avoid having to manually change it every time our data changes. This is a very powerful feature in VueJS and it allows us to change our data and see the changes reflected on the dom without modifying it.

For example, let's create another very basic app:

```html
<div id="TestApp">
  Hello, {{name}}, welcome to Vue
</div>
<script type="text/javascript">
  var testApp = new Vue({
    el: '#TestApp',
    data: {
      name: 'John'
    }
  })
</script>
```

That will render the following data at runtime:

```html
<div id="TestApp">
  Hello, John, welcome to Vue
</div>
```

Using the Vue instance, we can modify that data externally, and see the changes reflected on the DOM immediately:

```javascript
// On the console
testApp.name = 'Mike'
```

That will render the following data at runtime:

```html
<div id="TestApp">
  Hello, Mike, welcome to Vue
</div>
```

#### The v-if v-else directives

Alright, we're already familiar with data binding, a very powerful and clean feature that allows us to see our data being reflected on the DOM.

On VueJS, we have a conditional render directive, this allows us to render a chunk of our DOM if a condition is met, let's have the following example

```html
<div id="TestApp">
  Hello, {{name}}, welcome to Vue
  <div v-if="age > 22">
    {{name}} can drink a beer in most parts of the world
  </div>
  <div v-else>
    Sorry, no beer for you, {{name}}
  </div>
</div>
<script type="text/javascript">
  var testApp = new Vue({
    el: '#TestApp',
    data: {
      name: 'John',
      age: 21
    }
  })
</script>
```

If we increment John's age to 22, the v-if block will be met and rendered.

```javascript
// On the console
testApp.age = testApp.age + 1
```

**Note: Conditional rendering doesn't work by hiding or showing pieces of the DOM, it works by removing it or adding it back to the DOM, to use conditional show use the v-show directive**

#### The v-for directive

Creating collections and listed elements in Vue is very easy, the v-for directive allows us to bind a list to the dom.

```html
<div id="TestApp">
  Hello, {{name}}, welcome to Vue
  <ul>
    <li v-for="(drink, index) in favoriteDrinks" :key="index">
      {{drink}}
    </li>
  </ul>
</div>
<script type="text/javascript">
  var testApp = new Vue({
    el: '#TestApp',
    data: {
      name: 'John',
      age: 21,
      favoriteDrinks: [
        'Beer', 'Strawberry', 'Coke', 'Wine'
      ]
    }
  })
</script>
```

We can add or remove items to the favoriteDrinks array dynamically using Javascript array functions:

```javascript
// On the console

// Adding an element to the array
testApp.favoriteDrinks.push('Vodka')
// Removing an element from the array
testApp.favoriteDrinks.splice(testApp.favoriteDrinks.indexOf('Wine'), 1)
```

#### The vue instance: methods

The vue instance supports custom methods (functions) that allows us to perform custom operations over the data. Example:

```html
<div id="TestApp">
  Hello, {{name}}, welcome to Vue
  <div v-if="age > 22">
    {{name}} can drink a beer in most parts of the world
  </div>
  <div v-else>
    Sorry, no beer for you, {{name}}
  </div>
</div>
<script type="text/javascript">
  var testApp = new Vue({
    el: '#TestApp',
    data: {
      name: 'John',
      age: 21
    },
    methods: {
      incrementAge: function () {
        this.age = this.age + 1
      }
    }
  })
</script>
```

``` javascript
// On the console:
testApp.incrementAge()
```

You can also define parameters on your methods:

``` javascript
incrementAge: function (amount) {
  this.age = this.age + amount
}

// On the console:
testApp.incrementAge(5)
```

#### The v-on directive

The v-on directive allows us to bind a method on our vue instance to a HTML event.

**Note: v-on can be rewritten with the @ shorthand**

Example:

```html
<div id="TestApp">
  Hello, {{name}}, welcome to Vue
  <button v-on:click="incrementAge">Increment {{name}}'s age</button>
  <div v-if="age > 22">
    {{name}} can drink a beer in most parts of the world
  </div>
  <div v-else>
    Sorry, no beer for you, {{name}}
  </div>
</div>
<script type="text/javascript">
  var testApp = new Vue({
    el: '#TestApp',
    data: {
      name: 'John',
      age: 21
    },
    methods: {
      incrementAge: function () {
        this.age = this.age + 1
      }
    }
  })
</script>
```

#### The vue instance: computed properties

Computed properties allows us to bind our DOM to computed data, we could achieve the same using methods, but the difference here is that the VUE instance caches our computed properties in order to achieve the best possible performance.

In the following example, we are going to bind our data to all the drinks that start with B:

```html
<div id="TestApp">
  Hello, {{name}}, welcome to Vue
  <ul>
    <li v-for="(drink, index) in favoriteDrinks" :key="index">
      {{drink}}
    </li>
  </ul>
  <h2>Drinks starting with B</h2>
  <ul>
    <li v-for="(drinkWithB, index) in drinksStartingWithB" :key="index">
      {{drinkWithB}}
    </li>
  </ul>
</div>
<script type="text/javascript">
  var testApp = new Vue({
    el: '#TestApp',
    data: {
      name: 'John',
      age: 21,
      favoriteDrinks: [
        'Beer', 'Strawberry', 'Coke', 'Wine', 'Bourbon'
      ]
    },
    computed: {
      drinksStartingWithB: function () {
        return this.favoriteDrinks.filter(function (drink) {
          return drink.indexOf('b') == 0 || drink.indexOf('B') == 0
        })
      }
    }
  })
</script>
```

#### Data binding: Two way data binding and the v-model directive

In VueJS, performing two-way data binding with form values is very easy, this feature allows us to bind a variable to an input, allowing the variable to be binded to a form value and to the data at the same time.

Example:

```html
<div id="TestApp">
  Hello, {{name}}, welcome to Vue
  <label for="nameBox">Name</label>
  <input id="nameBox" type="text" v-model="name" />
  <div v-if="age > 22">
    {{name}} can drink a beer in most parts of the world
  </div>
  <div v-else>
    Sorry, no beer for you, {{name}}
  </div>
</div>
<script type="text/javascript">
  var testApp = new Vue({
    el: '#TestApp',
    data: {
      name: 'John',
      age: 21
    }
  })
</script>
```

This will update our bindings to the name immediately as we type on the text box.

**For number textboxes: use v-model.number to bind the value to a number, otherwise you will get a string binding on the input side.**

#### Now that we understand the basics of Vue, we can take a look at our TODO example
