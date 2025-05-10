<template>
	<date-picker
	  v-model="localValue"
	  format="YYYY-MM-DD"
	  display-format="jYYYY-jMM-jDD"
	  @change="handleChange"
	  class="jalali-date-picker"
	  simple
	/>
  </template>
  
  <script>
  import DatePicker from 'vue3-persian-datetime-picker'
  import dayjs from 'dayjs';
  import "./styles.css"
  
  export default {
	inject: ['values'],
	emits: ['input'],
	props: {
    value: {
      type: String,
      default: null
    }
  },
	data() {
	  return {
		localValue: this.value ||  dayjs().format('YYYY-MM-DD') 
	}
	},
	watch: {
	value(newValue) {
		this.localValue = newValue;
	}
	},
	methods: {
		handleChange(value, field) {
		if (field == this.field) {
			const localDate = dayjs(value).startOf('day').format('YYYY-MM-DD');
			this.$emit('input', localDate); 
		}
		}
	},
	name: "jalali-date-picker",
	components: { DatePicker }
  }
  </script>

  