<script setup>
import { ref, computed, watch } from 'vue'

const props = defineProps({
    regexStr: { type: String, required: true }
})

const emit = defineEmits(['inputs-updated', 'simulate-string'])

const userInputs = ref('')

watch(userInputs, (newVal) => {
    emit('inputs-updated', [newVal])
}, { deep: true })

const inputResult = computed(() => {
    if (!props.regexStr) {
        return 'No Regex'
    }

    try {
        // Remove spaces from regex and convert automata notation to JavaScript regex
        const cleanedRegex = props.regexStr.replace(/\s+/g, '')
        const jsRegexStr = '^' + cleanedRegex.split('+').join('|') + '$'
        const regex = new RegExp(jsRegexStr)

        if (userInputs.value === null || userInputs.value === undefined) return null
        const isValid = regex.test(userInputs.value)
        if (!isValid && userInputs.value === '') return 'null string not accepted'
        return isValid ? 'Valid' : 'Invalid'
    } catch (e) {
        console.error("Invalid Regex generated:", e)
        return 'Error'
    }
})
</script>

<template>
  <div class="input-area-container">
    <div class="inputs-area">
      <div class="input-row">
        <input
          v-model="userInputs"
          placeholder="Enter test string"
          class="input-field"
        />

        <span
          v-if="inputResult !== null"
          :class="[
            'result-badge',
            inputResult === 'Valid' ? 'valid' : 'invalid'
          ]"
        >
          {{ inputResult }}
        </span>

        <button
          @click="$emit('simulate-string', userInputs)"
          class="simulate-btn"
        >
          Simulate
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped src="../styles/InputArea.css"></style>