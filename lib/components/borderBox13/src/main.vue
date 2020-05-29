<template>
  <div class="dv-border-box-13" :ref="ref">
    <svg class="dv-border-svg-container" :width="width" :height="height">
      <path
        :fill="backgroundColor"
        :fill-opacity="backgroundColorOpacity"
        :stroke="mergedColor[0]"
        :stroke-width="borderWidth"
        :d="`
          M 5 20 L 5 10 L 12 3  L ${cornerBorderWidth * 10 + 50} 3 L ${cornerBorderWidth * 10 + 58} 10
          L ${width - 20} 10 L ${width - 5} 25
          L ${width - 5} ${height - 5} L 20 ${height - 5}
          L 5 ${height - 20} L 5 20
        `"
      />

      <path
        fill="transparent"
        stroke-linecap="round"
        :stroke-width="`${cornerBorderWidth / 2 + 2}`"
        :stroke-dasharray="dashArray"
        :stroke="mergedColor[0]"
        :d="`M 16 ${cornerBorderWidth * 1 + 9} L ${dashWidth} ${cornerBorderWidth * 1 + 9}`"
      />

      <path
        fill="transparent"
        :stroke="mergedColor[1]"
        :stroke-width="cornerBorderWidth"
        :d="`M 5 20 L 5 10 L 12 3  L ${cornerBorderWidth * 10 + 50} 3 L ${cornerBorderWidth * 10 + 58} 10`"
      />

      <path
        fill="transparent"
        :stroke="mergedColor[1]"
        :stroke-width="cornerBorderWidth"
        :d="`M ${width - 5} ${height - 30} L ${width - 5} ${height - 5} L ${width - 30} ${height - 5}`"
      />
    </svg>

    <div class="border-box-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import autoResize from '../../../mixin/autoResize'

import { deepMerge } from '@jiaminghi/charts/lib/util/index'

import { deepClone } from '@jiaminghi/c-render/lib/plugin/util'

export default {
  name: 'DvBorderBox13',
  mixins: [autoResize],
  props: {
    color: {
      type: Array,
      default: () => ([])
    },
    backgroundColor: {
      type: String,
      default: 'transparent'
    },
    backgroundColorOpacity: {
      type: Number,
      default: 1
    },
    cornerBorderWidth: {
      type: Number,
      default: 2
    },
    borderWidth: {
      type: Number,
      default: 1
    },
    dashArray: {
      type: String,
      default: "10, 5"
    },
    dashWidth: {
      type: Number,
      default: 61
    },
  },
  data () {
    return {
      ref: 'border-box-13',

      defaultColor: ['#6586ec', '#2cf7fe'],

      mergedColor: []
    }
  },
  watch: {
    color () {
      const { mergeColor } = this

      mergeColor()
    }
  },
  methods: {
    mergeColor () {
      const { color, defaultColor } = this

      this.mergedColor = deepMerge(deepClone(defaultColor, true), color || [])
    }
  },
  mounted () {
    const { mergeColor } = this

    mergeColor()
  }
}
</script>