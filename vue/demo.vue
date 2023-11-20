<template>
    <div>
      <v-container>
        <j-input label="J-Input" label-bg-color="#CCC" v-model="input"></j-input>
        <j-date v-model="date1"></j-date>
        <j-time v-model="time"></j-time>
        <j-select v-model="select" :options="options"></j-select>
        <j-radio v-model="radio" :options="options"></j-radio>
        <j-checkbox v-model="checkbox" :options="options"></j-checkbox>
        <j-number v-model="number"></j-number>
        <v-btn @click="onSubmit">ok</v-btn>
      </v-container>
    </div>
  </template>
  
  <script lang="ts" setup>
  
  import JInput from "@/components/Input.vue"
  import JDate from "@/components/Date.vue"
  import JTime from "@/components/Time.vue"
  import JSelect from "@/components/Select.vue"
  import type { Option } from "../components/Select.vue"
  import JRadio from "@/components/Radio.vue"
  import JCheckbox from "@/components/Checkbox.vue"
  import JNumber from "@/components/Number.vue"
  
  const input = ref("this is a input")
  const date1 = ref("")
  const time = ref("")
  const radio = ref(2)
  const select = ref(1)
  const checkbox = ref([1,2])
  const number = ref(1)
  
  const options: Option[] = [{
    label: "label",
    value: 1
  },{
    label: "label2",
    value: 2
  },{
    label: "label3",
    value: 3
  }]
  
  const onSubmit = () => console.log( select.value,  checkbox.value)
  
  </script>
