<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-grey-11">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
        <img width="45px" src="data:image/svg+xml;base64,PHN2ZyBpZD0iTGF5ZXJfMSIgZGF0YS1uYW1lPSJMYXllciAxIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyOTMgMjkzIj48ZGVmcz48c3R5bGU+LmNscy0xe2ZpbGw6IzY3ZmNiODt9LmNscy0ye2ZpbGw6IzNmM2YzZjt9PC9zdHlsZT48L2RlZnM+PHRpdGxlPmxvZ288L3RpdGxlPjxyZWN0IGNsYXNzPSJjbHMtMSIgd2lkdGg9IjI5MyIgaGVpZ2h0PSIyOTMiIHJ4PSI2MC45MiIvPjxwYXRoIGNsYXNzPSJjbHMtMiIgZD0iTTUwLjEsMTQ3LjQ3QTk3LjIyLDk3LjIyLDAsMCwxLDIzMSw5OGE4LjU1LDguNTUsMCwxLDAsMTQuNzEtOC43MkExMTQuMzQsMTE0LjM0LDAsMCwwLDM0Ljc4LDE2Ny42M2E4LjU1LDguNTUsMCwxLDAsMTYuODMtM0E5OC4xOSw5OC4xOSwwLDAsMSw1MC4xLDE0Ny40N1oiIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjgxIC0wLjk3KSIvPjxwYXRoIGNsYXNzPSJjbHMtMiIgZD0iTTI1My4wNywxMzguOTJhOC41NSw4LjU1LDAsMCwwLTguNTUsOC41NSw5Ny4wNiw5Ny4wNiwwLDAsMS04OC42Nyw5Ni44M2MwLS4xLDAtLjE5LDAtLjI5VjIwNi4zOWE1OS41NCw1OS41NCwwLDEsMC0xNy4xLDBWMjQ0YzAsLjEsMCwuMiwwLC4zYTk2LjgsOTYuOCwwLDAsMS02Ny4xNC0zNS44Miw4LjU1LDguNTUsMCwxLDAtMTMuMzEsMTAuNzUsMTE0LjI4LDExNC4yOCwwLDAsMCwyMDMuMjktNzEuNzdBOC41NSw4LjU1LDAsMCwwLDI1My4wNywxMzguOTJabS0xNDguMiw4LjU1YTQyLjQ1LDQyLjQ1LDAsMSwxLDUxLDQxLjU4VjE2My43OWE4LjU1LDguNTUsMCwwLDAtMTcuMSwwdjI1LjI2QTQyLjUyLDQyLjUyLDAsMCwxLDEwNC44NywxNDcuNDdaIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC44MSAtMC45NykiLz48cGF0aCBjbGFzcz0iY2xzLTIiIGQ9Ik0xNzEuODIsMjMwLjE0YTguNTYsOC41NiwwLDAsMS0yLjY3LTE2LjY4LDY5Ljg0LDY5Ljg0LDAsMCwwLDAtMTMyLjY1LDguNTUsOC41NSwwLDAsMSw1LjM0LTE2LjI1LDg2Ljk0LDg2Ljk0LDAsMCwxLDAsMTY1LjE0QTguMzQsOC4zNCwwLDAsMSwxNzEuODIsMjMwLjE0WiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuODEgLTAuOTcpIi8+PHBhdGggY2xhc3M9ImNscy0yIiBkPSJNMTIyLjgxLDIzMC4xNGE4LjM2LDguMzYsMCwwLDEtMi42OC0uNDQsODYuOTQsODYuOTQsMCwwLDEsLjY4LTE2NS4zNkE4LjU1LDguNTUsMCwwLDEsMTI2LDgwLjYzYTY5Ljg0LDY5Ljg0LDAsMCwwLS41NCwxMzIuODMsOC41Niw4LjU2LDAsMCwxLTIuNjcsMTYuNjhaIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC44MSAtMC45NykiLz48L3N2Zz4=" alt="">
        <div class="text-h5 text-weight-bold text-grey-14 absolute-center">Planeters.net</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-8"
        >
          Essential Links
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'

const linksData = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
]

export default {
  name: 'MainLayout',
  components: { EssentialLink },
  data () {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData
    }
  }
}
</script>
