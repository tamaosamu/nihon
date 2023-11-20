<script lang="ts" setup>
import JInput from "./Input.vue"
import JNumber from "./Number.vue"

const props = defineProps({
  modelValue: {
    required: true,
    type: String,
  },
  hour: {
    type: Boolean,
    default: true
  },
  minute: {
    type: Boolean,
    default: true
  },
  second: {
    type: Boolean,
    default: true
  }
})

// update v-model
const emit = defineEmits(['update:modelValue'])
// dialog status value (shown/hidden)
const visible = ref(true)
// hour and minute and second of object
const time = reactive({
  hour: 0,
  min: 0,
  sec: 0
})

// click cancel event
const onCancel = () => {
  visible.value = false
}

// click submit event
// 1. update v-model value
// 2. dialog closed
const onSubmit = () => {
  const modelValue = [time.hour, time.min, time.sec].join(":")
  emit("update:modelValue", modelValue)
  visible.value = false
}

// document mounted after...
onMounted(() => {
  if (!props.modelValue) {
    const current = new Date
    time.hour = current.getHours()
    time.min = current.getMinutes()
    time.sec = current.getSeconds()
    onSubmit()
  }
})
</script>

<template>


  <v-dialog width="360" v-model="visible" :return-value.sync="visible">
    <template #activator="{ props }">
      <j-input 
      v-bind="props" 
      append-icon="mdi-clock-outline" 
      @click="visible = true" 
      :model-value="modelValue"></j-input>
    </template>
    <v-card>
      <v-card-title>SELECT TIME</v-card-title>
      <v-card-text>
        <div class="card-content">
          <j-number  mode="column" align="center" input-width="60px" input-align="center" v-model="time.hour" :max-value="23"></j-number>
          <j-number  mode="column" align="center" input-width="60px" input-align="center" v-model="time.min" :max-value="59"></j-number>
          <j-number  mode="column" align="center" input-width="60px" input-align="center" v-model="time.sec" :max-value="59"></j-number>
        </div>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="onCancel">Cancel</v-btn>
        <v-btn @click="onSubmit">OK</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<style lang="scss" scoped>
.card-content {
  display: flex;
  justify-content: space-around;
}
</style>
