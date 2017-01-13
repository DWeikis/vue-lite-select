<template>
  <div id="app">
    <lite-select
            v-model="user"
            placeholder="Pick User"
            :options="users"
            loadFrom="https://jsonplaceholder.typicode.com/users"
    ></lite-select>
    User selected: {{ this.user }}
  </div>
</template>

<script>
import LiteSelect from './components/Select'

export default {
  name: 'app',
  components: {
    LiteSelect
  },
  data () {
    return {
      users: [
        { id: 1, name: 'John' },
        { id: 2, name: 'Jane' }
      ],
      user: null
    }
  }
}
</script>

