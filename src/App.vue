<template>
  <div id="app">
    <simple-select
            v-model="user"
            placeholder="Pick User"
            :options="users"
            loadFrom="https://jsonplaceholder.typicode.com/users"
    ></simple-select>
    User selected: {{ this.user }}
  </div>
</template>

<script>
import SimpleSelect from './components/Select'

export default {
  name: 'app',
  components: {
    SimpleSelect
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

