# vue-passport

A Vue component to display a dropdown select easily

## Install / Usage
``` bash
$ npm install vue-simple-select
```

```html
<template>
   <div id="app">
      <simple-select 
            v-model="user"
            placeholder="Pick User"
            :options="users"
      ></simple-select >
   </div>
</template>

<script>
import SimpleSelect from 'vue-simple-select'
export default {
  components: { SimpleSelect },
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
```

## Optional props
``` bash
/* 
 * Passing a placeholder, option with value 0 will be prepended 
 */
placeholder: String,

/* 
 * You can pass an api url to get the data asynchronously 
 */
loadFrom: {
  type: [String, Boolean],
  default: false
},

/* 
 * The field that will be used in the option value
 */
keyField: {
  type: String,
  default: 'id'
},

/* 
 * The field that will be used in the label value
 */
nameField: {
  type: String,
  default: 'name'
},

/* 
 * The options to be displayed
 */
options: {
  type: Array,
  default: function () { return [] }
}

```

