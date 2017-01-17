<script lang="babel">
import axios from 'axios'

import FrameworkWrapper from './FrameworkWrapper.vue'

export default {
  components: {
    FrameworkWrapper
  },
  data () {
    return {
      items: [],
      selected: ''
    }
  },
  props: {
    value: {
      default: ''
    },
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
    },
    frameworkCss: {
      type: [String, Boolean],
      default: false
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
    updateValue () {
      let selectedItem = this.items.find(item => item[this.keyField] === this.selected)

      this.$emit('input', this.selected)
      this.$emit('selected', selectedItem || {})
    }
  },
  watch: {
    options (options) {
      this.items = options
      this.selected = ''
    },
    value (value) {
      this.selected = value
    }
  }
}
</script>

<template>
    <framework-wrapper :fw="frameworkCss">
        <select
                v-model="selected"
                @change="updateValue"
                :class="{ 'form-group' : frameworkCss == 'bootstrap' }"
        >
            <option v-if="placeholder" value="">{{ placeholder }}</option>
            <option
                    v-for="item in items"
                    :value="item[keyField]"
            >{{ item[nameField] }}</option>
        </select>
    </framework-wrapper>
</template>
