
<script>
	export let label;
	export let value = '';
	export let disabled = false;
	export let isSecondaryColor = false;
	export let placeholder = false;
	export let isHighlighted = false;
	export let isInvalid = false;
	export let displaySizeOrMargin = false;
	export let setDisplaySizeOrMargin;
	export let onChangeValue;
</script>

<style>

	@keyframes shake {
  0% { transform: translate(1px, 1px) rotate(0deg); }
  10% { transform: translate(-1px, -2px) rotate(-1deg); }
  20% { transform: translate(-3px, 0px) rotate(1deg); }
  30% { transform: translate(3px, 2px) rotate(0deg); }
  40% { transform: translate(1px, -1px) rotate(1deg); }
  50% { transform: translate(-1px, 2px) rotate(-1deg); }
  60% { transform: translate(-3px, 1px) rotate(0deg); }
  70% { transform: translate(3px, 1px) rotate(-1deg); }
  80% { transform: translate(-1px, -1px) rotate(1deg); }
  90% { transform: translate(1px, 2px) rotate(0deg); }
  100% { transform: translate(0, 0) rotate(0deg); }
}

	.input-wrapper {
		height: 42px;
		position: relative;
		font-size: 85%;
		display: flex;
		justify-content: flex-end;
		background-color: var(--layer50);
		border: 1px solid var(--layer200);
		caret-color: var(--primary);
		border-radius: 6px;
	}
	.input-wrapper.invalid {
		animation: shake 0.5s cubic-bezier(.36,.07,.19,.97) both;
	}

	input {
		height: 100%;
		width: 75%;
		box-sizing: border-box;
		text-align: right;
		padding-right: 14px;
		font-size: inherit;
		font-weight: 600;
		/*transition: padding 200ms ease-in-out;*/
	}
	input:hover {
		border-color: var(--layer300);
	}
	input:focus, input.highlighted {
		border-color: var(--primary);
	}
	input:disabled {
		color: var(--text200);
	}	
	input.secondaryColor:focus, input.secondaryColor.highlighted {
		border-color: var(--secondary);
		caret-color: var(--secondary);
	}
	.invalid input {
		border-color: var(--secondary);
	}

	input::placeholder {
	  color: var(--text500);
	  opacity: 1;
	}
	input::-ms-input-placeholder{
	  color: var(--text500);
	}
	input:-ms-input-placeholder {
	  color: var(--text500);
	}

	.prefix {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		white-space: nowrap;
		left: 14px;
		display: flex;
		align-items: center;
		text-transform: uppercase;
		letter-spacing: 0.05rem;
		font-weight: 500;
		border: none;
		background-color: var(--layer50);
		outline: none;
	}
	.prefix:active, .prefix:focus {
		border: none;
		outline: none;
	}

</style>

<div class='input-wrapper' class:invalid={isInvalid} on:click|stopPropagation>
	<select class='prefix' title="Size/Margin" on:change={(e) => setDisplaySizeOrMargin(e.target.value)} value={displaySizeOrMargin}>
		<option>Size</option>
		<option>Margin</option>
	</select>
	<input id={label} type='number' step="0.0000001" value={value} on:change={newValue => onChangeValue(newValue.target.value)} min="0" max="10000000" maxlength="10" spellcheck="false" placeholder={placeholder || `0.0`} autocomplete="off" autocorrect="off" inputmode="decimal" lang="en" disabled={disabled}  class:secondaryColor={isSecondaryColor} class:highlighted={isHighlighted} >
</div>