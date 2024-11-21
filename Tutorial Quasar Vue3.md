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



