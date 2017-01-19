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
      selected: '',
      selectContainer: false,
      search: ''
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
  mounted () {
    // this.listenOutSideClick()
  },
  methods: {
    updateValue (id) {
      document.querySelector('.input-search').focus()
      this.search = this.items[this.items.findIndex(item => item.id === id)].name
      let selectedItem = this.items.find(item => item[this.keyField] === id)

      this.$emit('input', id)
      this.$emit('selected', selectedItem || {})
    },
    showSelectContainer () {
      if (this.selectContainer === true) {
        this.selectContainer = false
      } else {
        this.selectContainer = true
      }
    },
    filteredOptions () {
      if (!this.search) {
        return this.items
      }
      return this.items.filter(item => {
        return item.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
    }
    /* listenOutSideClick () {
      var self = this
      document.addEventListener('click', (event) => {
        if (!document.querySelector('.input-search').contains(event.target)) {
          self.selectContainer = false
        }
      })
    }, */
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
      <div class="select-search">
      <form>
        <input v-on:change="filteredOptions()" class="input-search" v-model="search" v-on:click="showSelectContainer()" placeholder="placeholder">
        <div v-show="selectContainer" class="select-container">
          <div class="select-options" v-for="item in filteredOptions()" v-on:click="updateValue(item[keyField])">{{ item[nameField] }}</div>
        </div>
      </div>
      </form>
    </framework-wrapper>
</template>
<style>
ul {
  list-style:none;
  text-decoration: none;
}

input:focus {
  border: 1px solid transparent;
  outline: none;
}

.select-search {
  background: white;
  width: 200px;
  height: auto;
  border: 2px solid #d5d5d5;
  border-radius: 2px 2px 0 0
}
.input-search {
  background: white;
  position: relative;
  z-index: 2;
  padding: 8px;
  width: auto; 
  border: 2px solid transparent;
  border-radius: 2px 2px 0 0
}
.select-container {
  z-index: 1;
  margin: 0 -2px;
  width: 200px;
  height: auto;
  max-height: 200px;
  overflow-y: scroll;
  border: 2px solid #d5d5d5;
  border-top: 1px solid #d5d5d5;
  background: white;
  border-radius: 0 0 2px 2px;
  outline: 0;
  position: absolute;
  -webkit-animation-name: slideInDown;
  animation-name: slideInDown;
  -webkit-animation-duration: .3s;
  animation-duration: .3s;
}
.select-options {
  padding: 7px;
  width: auto;
  border-bottom: 1px solid #f5f5f5;
  cursor: pointer;
}

@-webkit-keyframes slideInDown {
  from {
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
    visibility: visible;
  }

  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes slideInDown {
  from {
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
    visibility: visible;
  }

  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}
</style>