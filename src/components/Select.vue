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
    updateValue (event) {
      let id = event.target.value
      let selectedItem = this.items.find(item => item[this.keyField] == id)

      this.$emit('input', id)
      this.$emit('selected', selectedItem ? selectedItem : {})
    }
  },
  watch: {
    options(options) {
      this.items = options
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
