<script>
  import { createEventDispatcher } from "svelte";
  import PhonePrefixCombo from "../shared/PhonePrefixCombo.svelte";
  import FormInput from "./input/TextInput.svelte";
  import Label from "./structure/Label.svelte";

  const dispatch = createEventDispatcher();

  export let phone = "";

  let phonePrefix = "";

  $: updatePhonePrefix(phone);

  function onPhonePrefixChange(ev) {
    const { detail: newPrefix } = ev;

    let thePhone = phone;
    if (phonePrefix) thePhone = thePhone.substr(phonePrefix.length + 1);

    phonePrefix = newPrefix;

    dispatch("input", `${newPrefix && (newPrefix + " " || "")}${thePhone}`);
  }

  function updatePhonePrefix(thePhone) {
    console.log("Updating phone prefix", thePhone);

    if (!thePhone) return "";

    const [_, match] = new RegExp(/^(\+\d{1,3})?/).exec(thePhone);

    phonePrefix = match;
  }
</script>

<div class="row">
  <div class="col-md-5">
    <PhonePrefixCombo value={phonePrefix} on:change={onPhonePrefixChange} />
  </div>
  <div class="col-md-7">
    <Label inputId="phone-number">
      <span>Phone</span>
    </Label>

    <FormInput
      value={phone}
      name="phone"
      id="phone-number"
      type="tel"
      title="Enter phone in format: +123 123123123"
      placeholder="Your contact phone"
      on:input
    />
  </div>
</div>
