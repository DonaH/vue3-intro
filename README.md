## Vue 3 Basic 

## Simple Product App

### Overview of Topics
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
### Resources:
[Official Vue 3 site](https://v3.vuejs.org/guide/introduction.html)
[VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/intro-to-vue3)
[VueMastery Courses](https://www.vuemastery.com/courses/)
[VueMastery Repo to code along](https://github.com/Code-Pop/Intro-to-Vue-3)

---

### Details for Each Topic

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

    :open_file_folder: main.js
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

    :open_file_folder: index.html
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
  :open_file_folder: main.js
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
    :open_file_folder: index.html
    ```
    <p v-if="inStock">In Stock</p>
    <p v-else>Out of Stock</p>
    ```
    ```
    <p v-show="inStock">In Stock</p>
    ```
    :open_file_folder: main.js
    ```
    const app = Vue.createApp({
        data() {
            return {
                ...
                inventory: 100 
        }
    ```
    :open_file_folder: index.html
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
  :open_file_folder: main.js
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
    :open_file_folder: index.html
    ```
    <ul>
      <li v-for="detail in details">{{ detail }}</li>
    </ul>
    ```
    :open_file_folder: main.js
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
    :open_file_folder: index.html
    ```
    <div v-for="variant in variants" :key="variant.id">{{ variant.color }}</div>
    ```


##### 6. Event Handling - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/event-handling-vue3)
  * Event Handling

    :open_file_folder: index.html
    ```
    <div class="cart">Cart({{ cart }})</div>
    ...
    <button class="button">Add to Cart</button>
    ```
    :open_file_folder: main.js
    ```
    data() {
      return {
        cart: 0,
        ...
      }
    }
    ```
    :open_file_folder: index.html
    ```
    <button class="button" v-on:click="run logic here">Add to Cart</button>
    ```
    Call the method on click:
    ```
    <button class="button" v-on:click="addToCart">Add to Cart</button>
    ```
    :open_file_folder: main.js
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
    :open_file_folder: main.js
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
    :open_file_folder: index.html
    ```
    <div v-for="variant in variants" :key="variant.id" @mouseover="updateImage(variant.image)">{{ variant.color }}</div>
    ```
    :open_file_folder: main.js
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
  :open_file_folder: index.html
  ```
  <div 
    v-for="variant in variants" 
    :key="variant.id" 
    @mouseover="updateImage(variant.image)" 
    class="color-circle" 
  </div>
  ```
  :open_file_folder: style.css
  ```
  .color-circle {
    width: 50px;
    height: 50px;
    margin-top: 8px;
    border: 2px solid #d8d8d8;
    border-radius: 50%;
  } 
  ```
  :open_file_folder: index.html
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
  > Add quotes if you want to use Kebab case:
  >```
  ><div :style="{ 'background-color': variant.color }></div>
  >```

* Style Binding: Objects
  :open_file_folder: index.html
  ```
  <div :style="styles"></div>
  ```
  :open_file_folder: main.js
  ```
  data() {
    return {
      styles: {
        color: 'green',
        fontSize: '14px'
      }
    }
  }

* Class Binding
  * Disable 'add to cart' when out of stock 
  * Make button look disabled

    :open_file_folder: index.html
    ```
    <button 
      class="button" 
      :disabled="!inStock" 
      v-on:click="addToCart">
      Add to Cart
    </button>
    ```
    :open_file_folder: style.css
    ```
    .disabledButton {
      background-color: #d8d8d8;
      cursor: not-allowed;
    }
    ```
  * Conditionally apply the class when out of stock

    :open_file_folder: index.html
    ```
    <button 
      class="button" 
      :class="{ disabledButton: !inStock }" 
      :disabled="!inStock" 
      @click="addToCart">
      Add to Cart
    </button>
    ```

* Multiple Class Names
  Conditionally add the `active` class

  :open_file_folder: index.html
  ```
  <div class="color-circle"
    :class="{ active: activeClass }">
  </div>
  ```
  :open_file_folder: main.js
  ```
  data() {
    return {
      activeClass: true
    }
  }
  ```
  Combined look:
  ```
  <div class="color-circle active"></div>
  ```

* Ternary Operators

  In-line example:
  ```
  <div :class="[ isActive ? activeClass : '' ]"></div>
  ```

##### 8. Computed Properties - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/computed-properties-vue3)
* Simple Computed Property

  :open_file_folder: main.js
  ```
  data() {
    return {
      product: 'Socks',
      brand: 'Vue Mastery'
  }
  ```
  :open_file_folder: index.html
  ```
  <h1>{{ brand + ' ' + product }}</h1>
  ```
  Compute the Brand and Product Together:
  :open_file_folder: index.html
  ```
  <h1>{{ title }}</h1>
  ```
  :open_file_folder: main.js
  ```
  ...
  computed: {
    title() {
      return this.brand + ' ' + this.product
    }
  }
  ```
* Computing Image & Quantity
  Add `quantity` property to the variant objects

  :open_file_folder: main.js
  ```
  data() {
    return {
      ...
      variants: [
        { id: 2234, color: 'green', image: './assets/images/socks_green.jpg', quantity: 50 },
        { id: 2235, color: 'blue', image: './assets/images/socks_blue.jpg', quantity: 0 },
      ]
    }
  }
  ```
  Replace `updateImage()` with new method `updateVariant()`
  :open_file_folder: index.html
  ```
  <div 
    v-for="(variant, index) in variants" 
    :key="variant.id" 
    @mouseover="updateVariant(index)" <! -- new method -->
    class="color-circle" 
    :style="{ backgroundColor: variant.color }">
  </div>
  ```
  Add new data property which will be updated to equal `index`
  :open_file_folder: main.js
  ```
  data() {
    return {
      ...
      selectedVariant: 0,
      ...
    }
  }
  ```
  :open_file_folder: main.js
  ```
  updateVariant(index) {
    this.selectedVariant = index
  }
  ```
  Delete `image` & `inStock` from data, replace with computed properties
  :open_file_folder: main.js
  ```
  computed: {
    ...
    image() {
      return this.variants[this.selectedVariant].image
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity
    }
  }
  ```

##### 9. components & Props - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/components-and-props-vue3)

##### Components
* Create ProductDisplay component
  :open_file_folder: components/ProductDisplay.js
  ```
  app.component('product-display', {})
  ```
* Template
  :open_file_folder: components/ProductDisplay.js
  ```
  app.component('product-display', {
    template: 
      /*html*/ 
      `<div class="product-display">
        <div class="product-container">
          <div class="product-image">
            <img v-bind:src="image">
          </div>
          <div class="product-info">
            <h1>{{ title }}</h1>
    
            <p v-if="inStock">In Stock</p>
            <p v-else>Out of Stock</p>
    
            <div 
              v-for="(variant, index) in variants" 
              :key="variant.id" 
              @mouseover="updateVariant(index)" 
              class="color-circle" 
              :style="{ backgroundColor: variant.color }">
            </div>
            
            <button 
              class="button" 
              :class="{ disabledButton: !inStock }" 
              :disabled="!inStock" 
              v-on:click="addToCart">
              Add to Cart
            </button>
          </div>
        </div>
      </div>`
  })
  ```
  > Notice the template literal *back ticks* ` `` `, /\*html\*/  & VSCode extension:es6-string-html, syntax highlighting should work in VSCode.

* Move `data` & `methods` from `main.js` to here
  :open_file_folder: components/ProductDisplay.js
  ```
  app.component('product-display', {
    template: 
      /*html*/ 
      `<div class="product-display">
        ...
      </div>`,
    data() {
      return {
          product: 'Socks',
          brand: 'Vue Mastery',
          selectedVariant: 0,
          details: ['50% cotton', '30% wool', '20% polyester'],
          variants: [
            { id: 2234, color: 'green', image: './assets/images/socks_green.jpg', quantity: 50 },
            { id: 2235, color: 'blue', image: './assets/images/socks_blue.jpg', quantity: 0 },
          ]
      }
    },
    methods: {
        addToCart() {
            this.cart += 1
        },
        updateVariant(index) {
            this.selectedVariant = index
        }
    },
    computed: {
        title() {
            return this.brand + ' ' + this.product
        },
        image() {
            return this.variants[this.selectedVariant].image
        },
        inStock() {
            return this.variants[this.selectedVariant].quantity
        }
    }
  })
  ```
* Cleaning up `main.js` - leaving only cart data & empty methods for now
  ```
  const app = Vue.createApp({
    data() {
      return {
        cart: 0,
      }
    },
    methods: {}
  })
  ```
* Importing the Component
  :open_file_folder: index.html
  ```
  <!-- Import Components -->
  <script src="./components/ProductDisplay.js"></script>
  ```
* Using it in the template:
  :open_file_folder: index.html
  ```
  <div id="app">
    <div class="nav-bar"></div>

    <div class="cart">Cart({{ cart }})</div>
    <product-display></product-display>
  </div>
  ```
* Example of reusable blocks - add two more `product-display` components
  :open_file_folder: index.html
  ```
  <div id="app">
    <div class="nav-bar"></div>

    <div class="cart">Cart({{ cart }})</div>
    <product-display></product-display>
    <product-display></product-display>
    <product-display></product-display>
  </div>
  ```
##### Props
* props are custom attributes for passing data into a component.

Giving component a prop - premium account 
  * set the type & if it's required
    :open_file_folder: main.js
    ```
    const app = Vue.createApp({
      data() {
        return {
          cart: 0,
          premium: true
        }
      }
    })
    ```
    :open_file_folder: components/ProductDisplay.js
    ```
    app.component('product-display', {
      props: {
        premium: {
          type: Boolean,
          required: true
        }
      },
      ...
    }
    ```
  * Add custom attribute to `product-display` component
  :open_file_folder: index.html
    ```
    <div id="app">
    <div class="nav-bar"></div>

    <div class="cart">Cart({{ cart }})</div>
      <product-display :premium="premium"></product-display>
    </div>
    ```
  * Conditionally display shipping cost - if `premium` is `true`, shipping is free, otherwise, $2.99
  :open_file_folder: components/ProductDisplay.js
    ```
    template: 
    /*html*/
    `<div class="product-display">
      ...
        <p>Shipping: {{ shipping }}</p>
      ...
    </div>`,
    ```
    :open_file_folder: components/ProductDisplay.js
    ```
    computed: {
      ...
      shipping() {
        if (this.premium) {
          return 'Free'
        }
          return 2.99
        }
    }
    ```
##### 10. Communicating Events - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/communicating-events-vue3)
* Emitting the event - from product display component to `main.js` so we can update the cart
  :open_file_folder: components/ProductDisplay.js
  ```
  methods: {
    addToCart() {
      this.$emit('add-to-cart')
    }
    ...
  }
  ```
  :open_file_folder: index.html
  ```
  <product-display :premium="premium" @add-to-cart="updateCart"></product-display>
  ```
* Add `updateCart()` method in `main.js`
  :open_file_folder: main.js
  ```
  const app = Vue.createApp({
    data() {
      return {
        cart: [],
        ...
      }
    },
    methods: {
      updateCart() {
        this.cart += 1
      }
    }
  })
  ```
* Add product `id` to the cart
  :open_file_folder: main.js
  ```
  const app = Vue.createApp({
    data() {
      return {
        cart: [],
        ...
      }
    },
    methods: {
      updateCart(id) {
        this.cart.push(id)
      }
    }
    ```
* Add a payload to `add-to-cart` event emission, so `updateCart` has access to that `id`
  :open_file_folder: components/ProductDisplay.js
  ```
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].id)
    }
    ...
  }
  ```
* Since no need to display the `id` in the cart, we can use `.length` method to display the amount of items instead
  ```
  <div id="app">
  ...
  <div class="cart">Cart({{ cart.length }})</div>
  ...
  </div>
  ```

##### 11. Forms & v-model - [VueMastery Video](https://www.vuemastery.com/courses/intro-to-vue-3/forms-and-v-model-vue3)
* Add a Product Review Form with Two-way Binding: `v-model`

* Create new component - ReviewForm.js 
  :open_file_folder: components/ReviewForm.js
  ```
  app.component('review-form', {
  template:
  /*html*/
  `<form class="review-form">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name">

    <label for="review">Review:</label>      
    <textarea id="review"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <input class="button" type="submit" value="Submit">
  </form>`,
    data() {
      return {
        name: '',
        review: '',
        rating: null
      }
    }
  })
  ```
* Inside of the template, notice these elements:
  * `<input id="name">`
  * `<textarea id="review">`
  * `<select id="rating">`

* Bind these input fields to their respective data properties
  ```
    data() {
    return {
      name: '',
      review: '',
      rating: null
    }
  }
  ```

* Add `v-model` directive to each of these input elements
  :open_file_folder: components/ReviewForm.js
  ```
  app.component('review-form', {
  template:
  /*html*/
  `<form class="review-form">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="name">

    <label for="review">Review:</label>      
    <textarea id="review" v-model="review"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <input class="button" type="submit" value="Submit">  
    </form>`,
    data() {
      return {
        name: '',
        review: '',
        rating: null
    }
  })
  ```
  > Notice how on the \<select> element, we used `v-model.number` this is a modifier that typecasts the value as a number.

* Submitting the Review Form
  * Add a listener
    :open_file_folder: components/ReviewForm.js
    ```
    app.component('review-form', {
    template:
    /*html*/
    `<form class="review-form" @submit.prevent="onSubmit">
      ...
      <input class="button" type="submit" value="Submit">  
      </form>`
      ...
    })
    ```
  * Add `onSubmit()` method
    :open_file_folder: components/ReviewForm.js
    ```
    ...
    data() {
      return {
        name: '',
        review: '',
        rating: null
      }
    },
    methods: {
      onSubmit() {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
        }
        this.$emit('review-submitted', productReview)

        this.name = ''
        this.review = ''
        this.rating = null
      }
    }
    ...
    ```
  * Import the Review Form 
    :open_file_folder: index.html
    ```
    <!-- Import Components -->
    ...
    <script src="./components/ReviewForm.js"></script>
    ...
    ```
  * Use `review-form` component inside Product Display
    :open_file_folder: components/ProductDisplay.js
    ```
    template: 
    /*html*/
    `<div class="product-display">
      <div class="product-container">
      ...
      </div>
      <review-form></review-form>
      </div>`
    })
    ```
* Adding Product Reviews
  * Add event listener onto the `review-form`
    :open_file_folder: components/ProductDisplay.js
    ```
    template: 
    /*html*/
    `<div class="product-display">
      <div class="product-container">
      ...
      </div>
      <review-form @review-submitted="addReview"></review-form>
      </div>`
    })
    ```
  * Add a new `addReview()` method
    :open_file_folder: components/ProductDisplay.js
    ```
    ...
    data() {
      return {
        ...
        reviews: []
      }
    },
    methods: {
      ...
      addReview(review) {
        this.reviews.push(review)
      }
    },
    ...
    ```
* Displaying the reviews
  * Create new component - ReviewList.js to show the product review
    :open_file_folder: components/ReviewList.js
    ```
    app.component('review-list', {
    props: {
      reviews: {
        type: Array,
        required: true
      }
    },
    template:
    /*html*/
    `
    <div class="review-container">
    <h3>Reviews:</h3>
      <ul>
        <li v-for="(review, index) in reviews" :key="index">
          {{ review.name }} gave this {{ review.rating }} stars
          <br/>
          "{{ review.review }}"
          <br/>
        </li>
      </ul>
    </div>
    `
    })
    ```
  * Import this new component
    :open_file_folder: index.html
    ```
    <!-- Import Components -->
    ...
    <script src="./components/ReviewList.js"></script>
    ...
    ```
    :open_file_folder: components/ProductDisplay.js
    ```
    template: 
      /*html*/
      `<div class="product-display">
        <div class="product-container">
        ...
        </div>
        <review-list :reviews="reviews"></review-list>
        <review-form @review submitted="addReview"></review-form>
      </div>`
    })
    ```
* Don't show the review if none is present using `.length` method 
  :open_file_folder: components/ProductDisplay.js
  ```
  template: 
    /*html*/
    `<div class="product-display">
      ...
      <review-list v-if="reviews.length" :reviews="reviews"></review-list>
      ...
    </div>`
  })
  ```

* Basic Form Validation
  :open_file_folder: components/ReviewForm.js
  ```
  methods: {
    onSubmit() {
      if (this.name === '' || this.review === '' || this.rating === null) {
        alert('Review is incomplete. Please fill out every field.')
        return
      }
    ...
    }
  }
  ```

---
* Last Modified On: 2021-08-09
* Creation Date: 2021-08-05