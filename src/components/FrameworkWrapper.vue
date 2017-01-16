<script lang="babel">
    export default{
        props: [
            'fw'
        ]
    }
</script>
<template>
    <p v-if="fw == 'bulma'" class="control is-expanded">
      <span class="select is-fullwidth">
        <slot></slot>
      </span>
    </p>
    <div  v-else>
        <slot></slot>
    </div>
</template>
