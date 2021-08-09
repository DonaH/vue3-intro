## Vue 3 Basic 

## Simple product app

### Overview of topics
1. Intro to Vue 3
2. Creating the Vue App
3. Attribute Binding
4. Conditional Rendering
5. List Rendering
6. Event Handling
7. Class & Style Binding
8. Computed Properties
9. components & Props
10. Communicating Events
11. Forms & v-model
---

### Details for each topic

##### 1. Intro to Vue 3 - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/intro-to-vue3)
  * Covers fundamentals of building a Vue app
  * Administer variations of product
  * Add to cart / remove from cart logic
  * In stock / out of stock logic
  * Build a review form with Vue
  * Recommended extension for VSCode:
    * es6-string-html by Tobermory

##### 2. Creating the Vue App - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/creating-the-vue-app-vue3)
  * Create Vue app:
  main
  ```
  const app = Vue.createApp({
    data() {
      return {
        product: 'Socks'
      }
    `}`
  })
  ```
  * Mount Vue app:
  index
  ```
  <html>
    <body>
      <div id="app"></div>

      <!-- Import App -->
      <script src="./main.js"></script>

      <!-- Mount App -->
      <script>const mountedApp = app.mount('#app')</script>
    </body>
  </html>
  ```
  * Once the app is mounted, you can run JavaScript Expression inside html file such as:
    ```
      <h1>{{ product }}</h1>
      <p>{{ firstName + ' ' + lastName }}</p>
      <span>{{ clicked ? true : false }}</span>
      <div>{{ message.method() }}</div>
    ```
  > **Reactivity System** underneath the hood will take care of the DOM updates. Learn more here >> [Reactivity in Depth](https://v3.vuejs.org/guide/reactivity.html#what-is-reactivity)

##### 3. Attribute Binding - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/attribute-binding-vue3)
  * Attribute binding example:
    ```
    <img v-bind:src="image">
    <img :src="image"> <!-- equivalent shorthand -->
    ```

  * More examples:
    ```
    <img :src="image">
    <img :alt="description">1
    <a :href="url">
    <div :class="isActive">
    <span :style="isActive">
    <span :disables="isDisabled">
    ```

##### 4. Conditional Rendering - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/conditional-rendering-vue3)
  * Directives: v-if | v-else | v-show
  main
    ```
      const app = Vue.createApp({
        data() {
            return {
                product: 'Socks',
                image: './assets/images/socks_blue.jpg',
                inStock: true 
            }
        }
      })
    ```
    index
    ```
    <p v-if="inStock">In Stock</p>
    <p v-else>Out of Stock</p>
    ```
    ```
    <p v-show="inStock">In Stock</p>
    ```
    main
    ```
    const app = Vue.createApp({
        data() {
            return {
                ...
                inventory: 100 
        }
    ```
    index
    ```
    <p v-if="inventory > 10">In Stock</p>
    <p v-else>Out of Stock</p>
    ```
    ```
    <p v-if="inventory > 10">In Stock</p>
    <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
    <p v-else>Out of Stock</p>
    ```

##### 5. List Rendering - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/list-rendering-vue3)
  * Looping through an array list and array of objects: v-for
  main
    ```
    const app = Vue.createApp({
        data() {
            return {
                ...
                details: ['50% cotton', '30% wool', '20% polyester']
            }
        }
    })
    ```
    index
    ```
    <ul>
      <li v-for="detail in details">{{ detail }}</li>
    </ul>
    ```
    main
    ```
    data() {
      return {
        ...
        variants: [
          { id: 2234, color: 'green' },
          { id: 2235, color: 'blue' }
        ]
      }
    }
    ```
    index
    ```
    <div v-for="variant in variants" :key="variant.id">{{ variant.color }}</div>
    ```


##### 6. Event Handling - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/event-handling-vue3)
  * Event Handling

    :file_folder: index.html
    ```
    <div class="cart">Cart({{ cart }})</div>
    ...
    <button class="button">Add to Cart</button>
    ```
    :file_folder: main.js
    ```
    data() {
      return {
        cart: 0,
        ...
      }
    }
    ```
    index
    ```
    <button class="button" v-on:click="run logic here">Add to Cart</button>
    ```
    Call the method on click:
    ```
    <button class="button" v-on:click="addToCart">Add to Cart</button>
    ```
    main
    ```
    const app = Vue.createApp({
      data() {
        return {
          cart: 0,
          ...
        }
      },
      methods: {
        addToCart() {
          this.cart += 1
        }
      }
    })
    ```
    Shorthand for 'v-on' is '@'
    ```
    <button class="button" @click="addToCart">Add to Cart</button>
    ```
    main
    ```
    data() {
      return {
        ...
        variants: [
          { id: 2234, color: 'green', image: './assets/images/socks_green.jpg' },
          { id: 2235, color: 'blue', image: './assets/images/socks_blue.jpg' },
        ]
      }
    }
    ```
    index
    ```
    <div v-for="variant in variants" :key="variant.id" @mouseover="updateImage(variant.image)">{{ variant.color }}</div>
    ```
    main
    ```
    methods: {
      ...
      updateImage(variantImage) {
        this.image = variantImage
      }
    }
    ```

##### 7. Class & Style Binding - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/class-and-style-binding-vue3)
* Style Binding
  index
  ```
  <div 
    v-for="variant in variants" 
    :key="variant.id" 
    @mouseover="updateImage(variant.image)" 
    class="color-circle" 
  </div>
  ```
  style.css
  ```
  .color-circle {
    width: 50px;
    height: 50px;
    margin-top: 8px;
    border: 2px solid #d8d8d8;
    border-radius: 50%;
  } 
  ```
  index
  ```
  <div 
    v-for="variant in variants" 
    :key="variant.id" 
    @mouseover="updateImage(variant.image)" 
    class="color-circle" 
    :style="{ backgroundColor: variant.color }">
  </div>
  ```
  Understanding Style Binding
  ```
  <div 
    ...
    :style="{ backgroundColor: variant.color }">
  </div>
  ```
  > ##### Camel vs Kebab
  >Use Camel case for css property inside JavaScript Expression:
  >```
  ><div :style="{ backgroundColor: variant.color }></div>
  >```
  >If you want to use Kebab case add quotes like this:
  >```
  ><div :style="{ 'background-color': variant.color }></div>
  >```

* Style Binding: Objects


* Class Binding


* Multiple Class Names


* Ternary Operators

##### 8. Computed Properties - [VueMastery Video]()
##### 9. components & Props - [VueMastery Video]()
##### 10. Communicating Events - [VueMastery Video]()
##### 11. Forms & v-model - [VueMastery Video]()

---
* Creation Date: 2021-08-05
* Modified Date: 2021-08-07