<template>
  <div class="j-input" :style="divStyle">
    <label :style="labelStyle" v-if="props.label">
      {{ props.label }}
    </label>
    <v-input v-bind="$attrs" :messages="props.messages" :append-icon="props.appendIcon">
      <input :style="inputStyle" :value="props.modelValue" @input="onInput" />
      <template v-if="prepend" #prepend><slot name="prepend"></slot></template>
      <template v-if="append" #append><slot name="append"></slot></template>
    </v-input>
  </div>
</template> 
<script lang="ts" setup>
import type { Property } from 'csstype';
import type { PropType } from 'vue';
import type { CSSProperties } from 'vue'; 

const props = defineProps({
  modelValue: {
    type: String,
    default: ""
  },
  label: {
    type: String,
    default: ""
  },
  labelWidth: {
    type: String,
    default: "auto"
  },
  labelAlign: {
    type: String as PropType<Property.TextAlign>,
    default: "right"
  },
  labelBgColor: {
    type: String,
    default: "unset"
  },
  inputWidth: {
    type: String,
    default: "100%"
  },
  inputAlign: {
    type: String as PropType<Property.TextAlign>,
    default: "right"
  },
  messages: {
    type: Array as PropType<string[]>,
    default: () => []
  },
  appendIcon: {
    type: String,
    default: ""
  },
  display: {
    type: String as PropType<Property.Display>,
    default: "flex"
  },
  prepend: {
    type: Boolean,
    default: false
  },
  append: {
    type: Boolean,
    default: false
  }
}) 
const divStyle: CSSProperties = {
  display: props.display
} 
const labelStyle: CSSProperties = {
  backgroundColor: props.labelBgColor,
  width: props.labelWidth ?? 'auto',
  justifyContent: props.labelAlign,
} 
const inputStyle: CSSProperties = {
  width: props.inputWidth ?? 'auto',
  textAlign: props.inputAlign
} 
const emit = defineEmits(['update:modelValue'])
const onInput = (e: any) => {
  emit("update:modelValue", e.target.value)
} 
onMounted(() => {
  
}) 
</script> 
<style lang="scss" scoped>
.j-input {
  label {
    display: flex;
    align-items: center;
    padding: 0 1rem;
  } 
  input {
    padding: 3px 1rem;
    outline: unset;
    border-color: #CCC;
    border-width: 1px;
    border-style: solid;
  } 
  label, input {
    height: 42px
  }
}
</style>
