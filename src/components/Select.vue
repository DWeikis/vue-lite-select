<script>
import axios from 'axios'

export default {
  data () {
    return {
      items: []
    }
  },
  props: {
    placeholder: String,
    loadFrom: {
      type: [String, Boolean],
      default: false
    },
    keyField: {
      type: String,
      default: 'id'
    },
    nameField: {
      type: String,
      default: 'name'
    },
    options: {
      type: Array,
      default: function () { return [] }
    }
  },
  created () {
    if (this.loadFrom) {
      axios.get(this.loadFrom)
          .then(({data}) => { this.items = data })
    } else {
      this.items = this.options
    }
  },
  methods: {
    updateValue (event) {
      this.$emit('input', event.target.value)
    }
  }
}
</script>

<template>
    <select @change="updateValue">
        <option v-if="placeholder" value="">{{ placeholder }} </option>
        <option
                v-for="item in items"
                :value="item[keyField]"
        >{{ item[nameField] }}</option>
    </select>
</template>
