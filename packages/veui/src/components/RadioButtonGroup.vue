<template>
<div class="veui-radio-button-group veui-button-group" :ui="ui">
  <veui-button
    :class="{
      'veui-button-selected': item.value === value
    }"
    :ui="buttonUI"
    v-for="(item, index) in items"
    :key="index"
    :disabled="item.disabled || realDisabled || realReadonly"
    @click="handleChange(item.value)">
    <slot v-bind="item">{{ item.label }}</slot>
  </veui-button>
</div>
</template>

<script>
import { input, ui } from '../mixins'
import { includes } from 'lodash'
import Button from './Button'

export default {
  name: 'veui-radio-button-group',
  components: {
    'veui-button': Button
  },
  mixins: [input, ui],
  model: {
    event: 'change'
  },
  props: {
    ui: String,
    items: Array,
    value: null
  },
  computed: {
    buttonUI () {
      let allowed = ['alt', 'tiny', 'small', 'large']
      return this.uiProps.filter(ui => includes(allowed, ui)).join(' ')
    }
  },
  methods: {
    handleChange (val) {
      if (this.val !== val) {
        this.$emit('change', val)
      }
    }
  }
}
</script>
