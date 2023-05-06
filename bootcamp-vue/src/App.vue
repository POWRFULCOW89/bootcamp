<script >
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import MyComponent from './components/Component.vue';
import TestView from './views/TestView.vue';
import Form from './components/Form.vue';

// const isHidden = true;

export default {
    data() {
        return {
            isHidden: false,
            items: Array(10).fill(0).map((_, i) => i + 1)
        };
    },
    methods: {
        // toggle: () => this.isHidden = !this.isHidden
        toggle() {
            this.isHidden = !this.isHidden;
        }
    },
    components: { MyComponent, TestView, Form }
}
</script>

<template>


<!-- <TestView/>

<button @click="toggle">Toggle</button>
<MyComponent/>
<my-component /> -->


<header v-bind:class="{ hide: isHidden }">
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <!-- <HelloWorld msg="You did it!" /> -->

      <!-- <ul>
        <li v-for="item in items" v-bind:key="item">
          {{ item }}
        </li>
      </ul> -->


<!-- <Form form-name="Formulario" :show-age="true"></Form> -->

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/api">API</RouterLink>
      </nav>
    </div>
  </header>

<Suspense>
  
  <RouterView />
</Suspense>
</template>

<style scoped>
.hide {
  display: none;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
