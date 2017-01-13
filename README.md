# vue-lite-select

A Vue component to display a dropdown select easily

## Install / Usage
``` bash
$ npm install vue-lite-select
```

```html
<template>
   <div id="app">
      <lite-select 
            v-model="user"
            placeholder="Pick User"
            :options="users"
      ></lite-select >
   </div>
</template>

<script>
import LiteSelect from 'vue-lite-select'
export default {
  components: { LiteSelect },
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

