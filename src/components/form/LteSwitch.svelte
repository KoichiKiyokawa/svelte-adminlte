﻿<script>
	// this, in fact, is not a LTE component (I just could not think of a different name :))

  import {createEventDispatcher} from "svelte"

  const dispatch = createEventDispatcher()

  export let checked = false
  export let checkedClass = ""
  export let uncheckedClass = ""

  $: sliderClasses = checked
	  && checkedClass
    || uncheckedClass
</script>

<label class="switch">
	<input type="checkbox" {checked} on:change={() => dispatch("change", !checked)} />
	<span class="slider {sliderClasses}"></span>
</label>

<style lang="sass">
	.switch
		position: relative
		display: inline-block
		width: 3rem
		height: 1.5rem
		margin: 0 !important

		input
			opacity: 0
			width: 0
			height: 0

	.slider
		position: absolute
		cursor: pointer
		top: 0
		left: 0
		right: 0
		bottom: 0
		background-color: #ccc
		border-radius: 1rem

		&:before
			position: absolute
			content: ""
			height: 1.3rem
			width: 1.3rem
			left: .1rem
			bottom: .1rem
			background-color: white
			-webkit-transition: 0.1s
			transition: 0.1s
			border-radius: 50%

	input:checked + .slider
		//background-color: #2196f3
		//box-shadow: 0 0 1px #2196f3

		&:before
			-webkit-transform: translateX(1.5rem)
			-ms-transform: translateX(1.5rem)
			transform: translateX(1.5rem)
</style>
