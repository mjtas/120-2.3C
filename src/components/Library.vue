<template>
    <div>
      <!-- 1. Template Syntax -->
      <h1>{{ libraryName }}</h1>
      <p v-html="libraryDescription"></p>
      <div :id="libraryId">{{ libraryId }}</div>
      <p>{{ `Books in ${libraryName}` }}</p>
  
      <!-- 2. Methods -->
      <button @click="loadBooks">Load Books</button>
  
      <!-- 3. Reactivity Fundamentals -->
      <p>{{ reactiveData }}</p>
  
      <!-- 4. Computed Properties -->
      <p>Cart Size: {{ cart.length }}</p>
  
      <!-- 5. Class and Style Bindings -->
      <div :class="{ active: isActive, 'text-danger': hasError }" :style="{ color: textColor }">
        Class and Style Bindings
      </div>
  
      <!-- 6. List Rendering -->
      <ul>
        <!-- a. v-for with an Object -->
        <li v-for="(book, index) in bookList" :key="index">{{ book.title }}</li>
  
        <!-- b. v-for with a Range -->
        <li v-for="n in cart.length" :key="n">{{ n }}</li>
  
        <!-- c. v-for on <template> -->
        <template v-for="(book, index) in bookList" :key="index">
          <li>{{ book.author }} - {{ book.title }}</li>
        </template>
  
        <!-- d. v-for with v-if -->
        <li v-for="book in bookListWithCondition" :key="book.id" v-if="book">
          {{ book.title }}
        </li>
  
        <!-- e. v-for with a Component -->
        <li v-for="book in bookList" :key="book.id">
        <button @click="selectBook(book)">{{ book.title }}</button>
        </li>
      </ul>

      <!-- 7. Event Handling: Listening to Events -->
      <button @click="addToCart">Add to Cart</button>
  
      <!-- 8. Form Input Bindings -->
      <input type="text" v-model="searchQuery" />
      <input type="checkbox" v-model="isAvailable" />
      <input type="radio" v-model="selectedCategory" value="fiction" />
      <input type="radio" v-model="selectedCategory" value="non-fiction" />
      <select v-model="selectedLanguage">
        <option value="english">English</option>
        <option value="spanish">Spanish</option>
      </select>
      <textarea v-model="bookDescription"></textarea>
  
      <!-- 9. Watchers -->
      <p>{{ searchQuery }}</p>
  
      <!-- 10. Components -->
      <div v-if="selectedBook">
        <book-details :book="selectedBook" @view-details="showBookDetails"></book-details>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, computed, watch } from 'vue';
  import BookDetails from './BookDetails.vue'; // Import BookDetails component
  import BookItem from './BookItem.vue'; // Import BookItem component
  
  export default {
    components: {
      BookDetails,
      BookItem,
    },
    data() {
      return {
        // 1. Template Syntax
        libraryName: 'My Library',
        libraryDescription: '<em>A great place to read!</em>',
        libraryId: 'library-123',
  
        // 2. Methods
        reactiveData: '',
  
        // 4. Computed Properties
        cart: [],
  
        // 5. Class and Style Bindings
        isActive: true,
        hasError: false,
        textColor: 'blue',
  
        // 6. List Rendering
        bookList: [
          { id: 1, title: 'Book 1', author: 'Author 1', available: true },
          { id: 2, title: 'Book 2', author: 'Author 2', available: false },
          { id: 3, title: 'Book 3', author: 'Author 3', available: true },
        ],
  
        // 8. Form Input Bindings
        searchQuery: '',
        isAvailable: false,
        selectedCategory: '',
        selectedLanguage: '',
        bookDescription: '',
  
        // 10. Components
        selectedBook: null,

        
      };
    },
    computed: {
      // 4. Computed Properties
      bookCount() {
        return this.books.length;
      },
  
      // 6. List Rendering
      bookListWithCondition() {
        return this.bookList.filter((book) => this.isAvailable || book.available);
      },

      // Storing filtered results
      filteredBookList() {
      return this.bookList.filter((book) =>
        book.title.toLowerCase().includes(this.searchQuery.toLowerCase()));
      },
    },

    methods: {
      // 2. Methods
      loadBooks() {
        this.reactiveData = 'Books loaded!';
      },
  
      // 7. Event Handling: Listening to Events
      addToCart(book) {
        this.cart.push(book);
      },
      // Handle book selection
      selectBook(book) {
      this.selectedBook = book;
      },
    },
    
    watch: {
    searchQuery(newValue, oldValue) {
      console.log(`Search query changed from "${oldValue}" to "${newValue}"`);
      this.selectedBook = null; // Reset the selected book when the search query changes
      },
    },
  };
  </script>
  