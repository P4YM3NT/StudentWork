# Tutorial Addressbook with Quasar & Vue3
In this tutorial, we'll build an address book application using Quasar and Vue 3's <script setup> syntax. This app will fetch contacts from a backend API, display them, and allow users to add new ones. Along the way, you'll learn about routing, components, state management with Pinia, and Axios for API calls.

## 1. Prerequisites
- Basic knowledge of Vue.js and JavaScript.
- Node.js installed on your system.
- Backend API ready to handle contacts (`name`, `email`, `phone`).

---

## 2. Setting Up Quasar

#### Install Quasar CLI
```bash
npm install -g @quasar/cli
```

#### Create a New Project
```bash
npm init quasar 
```
Follow the prompts to set up your project (choose Vue 3 and other defaults).

#### Start the Development Server
```bash
cd address-book-app
quasar dev
```

---

## 3. Setting Up Routing
In Quasar, routing is configured in `src/router/routes.js`.

Modify `routes.js`
Add routes for the main pages of the app:

```javascript
const routes = [
  {
    path: '/',
    component: () => import('layouts/MainLayout.vue'),
    children: [
      { path: '', component: () => import('pages/AddressBook.vue') },
      { path: '/add', component: () => import('pages/AddContact.vue') }
    ]
  }
];

export default routes;
```

---

## 4. Layout
In the Quasar Framework, Pages and Layouts are key components that structure the app, providing a clear separation of concerns and enabling flexibility.

#### 1. Layouts
- Purpose: Define the framework or skeleton of the app, such as the header, footer, sidebars, or navigation structure.
- Location: Found in the `src/layouts/` directory.
- Structure: Layouts contain slots for rendering pages and reusable components like headers or navigation drawers.
- Example: A common layout file like `MainLayout.vue` may look like this:

```javascript
<template>
  <q-layout view="lHh Lpr lFf">
    <!-- Header -->
    <q-header elevated>
      <q-toolbar>
        <q-btn flat icon="menu" @click="toggleDrawer" />
        <q-toolbar-title>My App</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <!-- Sidebar -->
    <q-drawer show-if-above v-model="drawer" side="left">
      <q-list>
        <q-item clickable v-ripple to="/">
          <q-item-section>Home</q-item-section>
        </q-item>
        <q-item clickable v-ripple to="/add">
          <q-item-section>Add Contact</q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- Page Container -->
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue';

const drawer = ref(false);
const toggleDrawer = () => (drawer.value = !drawer.value);
</script>
```

#### Key Points in the Example:
1. `<q-layout>`:
  - A root Quasar layout component. The view="lHh Lpr lFf" defines its structure:
    - lHh: Header, fixed position.
    - Lpr: Left drawer, responsive.
    - lFf: Footer, fixed.
2. `<q-header>`: A top navigation bar for branding or app-wide actions.
3. `<q-drawer>`: A sidebar component that can hold navigation or other controls.
4. `<router-view>`: A placeholder where the active page (from Vue Router) will render dynamically.
5. State Management:
- `drawer`: A reactive property controlling whether the sidebar is open.
- `toggleDrawer`: Toggles the drawer's visibility.

#### Routing Integration
Pages are connected to the layout through Vue Router. For example, in `src/router/routes.js`:

```javascript
export default [
  {
    path: '/',
    component: () => import('layouts/MainLayout.vue'),
    children: [
      { path: '', component: () => import('pages/Home.vue') },
      { path: 'add', component: () => import('pages/AddContact.vue') },
    ]
  }
];
```

- The `MainLayout` provides the overall structure.
- The `Home.vue` and `AddContact.vue` pages are rendered in the layout's `<router-view>` slot.

---

## 5. Pages in Quasar

In Quasar, pages represent the main content views that are displayed in the application based on the routing. Here's how you can create a functional Address Book page `(AddressBook.vue)` in Quasar, using the provided code as an example.

#### Address Book Page (`AddressBook.vue`)
The `AddressBook.vue` page is designed to:

1. Fetch a list of contacts from the backend.
2. Display these contacts in a list format.
3. Include a button to navigate to an "Add Contact" form.

```javascript
<template>
  <q-page padding>
    <!-- Add Contact Button -->
    <q-btn label="Add Contact" color="primary" @click="navigateToAdd" />

    <!-- Contacts List -->
    <q-list bordered padding>
      <q-item v-for="contact in contacts" :key="contact.id">
        <q-item-section>
          <div><strong>{{ contact.name }}</strong></div>
          <div>{{ contact.email }}</div>
          <div>{{ contact.phone }}</div>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useContactsStore } from 'src/stores/contacts';
import { useRouter } from 'vue-router';

const router = useRouter(); // Access Vue Router for navigation
const store = useContactsStore(); // Access the Pinia store for contacts
const contacts = ref([]); // Local state to hold contacts

// Fetch contacts from the backend when the component mounts
const fetchContacts = async () => {
  await store.fetchContacts(); // Calls the Pinia action
  contacts.value = store.contacts; // Updates the local state
};

// Lifecycle hook to load data
onMounted(fetchContacts);

// Navigation function to redirect to the Add Contact page
const navigateToAdd = () => {
  router.push('/add');
};
</script>
```

## Vuex Store Setup

1. Install Vuex (if not already installed):
Run the following command to add Vuex to your project:
```bash
npm install vuex
```

2. Create the Vuex Store
Create the store in a file called `src/store/index.js`:

```javascript
import { createStore } from 'vuex';
import axios from 'axios';

// Define the Vuex store
const store = createStore({
  state: {
    contacts: [] // Holds the list of contacts
  },
  mutations: {
    SET_CONTACTS(state, contacts) {
      // Updates the state with fetched contacts
      state.contacts = contacts;
    },
    ADD_CONTACT(state, contact) {
      // Adds a new contact to the state
      state.contacts.push(contact);
    }
  },
  actions: {
    async fetchContacts({ commit }) {
      // Fetches contacts from the backend
      try {
        const response = await axios.get('https://your-backend-url.com/contacts');
        commit('SET_CONTACTS', response.data); // Updates the state with fetched data
      } catch (error) {
        console.error('Error fetching contacts:', error);
      }
    },
    async addContact({ commit }, contact) {
      // Adds a new contact to the backend and updates the state
      try {
        const response = await axios.post('https://your-backend-url.com/contacts', contact, {
          headers: { 'Content-Type': 'application/json' }
        });
        commit('ADD_CONTACT', response.data); // Adds the new contact to the state
      } catch (error) {
        console.error('Error adding contact:', error);
      }
    }
  },
  getters: {
    // Getter to retrieve contacts from the state
    allContacts(state) {
      return state.contacts;
    }
  }
});

export default store;
```

#### How It Works
1. State Management:

- The `state` in Vuex holds the `contacts` array, which is the central source of truth for contact data.
- The `SET_CONTACTS` mutation updates the state when data is fetched.

2. Actions and Mutations:

- The `fetchContacts` action fetches data from the backend using Axios and commits the `SET_CONTACTS` mutation to update the state.
- The `addContact` action sends a POST request to add a new contact and updates the state by committing the `ADD_CONTACT` mutation.

3. Component Integration:

- The `contacts` list in the component is a computed property linked to the Vuex store via the `allContacts` getter.
- On mounting the component, the `fetchContacts` action is dispatched to load data into the Vuex store.

4. Dynamic Rendering:

- The `q-item` elements are dynamically rendered using `v-for` based on the `contacts` array from the Vuex store.

5. Routing:

- The `navigateToAdd` function uses the Vue Router to navigate to the `/add` page for adding new contacts.

#### Benefits of This Approach
- Centralized State: Vuex ensures that the contact data is consistent across all components.
- Scalability: The app can easily handle additional features or data sources by expanding the store.
- Separation of Concerns: The component focuses only on the UI and delegates data fetching to Vuex actions.
This structure is clean, modular, and follows best practices for Vue 3 applications.

--- 


