<script>
  import { createEventDispatcher } from 'svelte';

  import TextInput from '../UI/TextInput.svelte';
  import Button from '../UI/Button.svelte';

  let title = '';
  let subtitle = '';
  let address = '';
  let email = '';
  let description = '';
  let imageUrl = '';


  const dispatch = createEventDispatcher();

  function submitForm() {
    dispatch('save', {
      title,
      subtitle,
      address,
      email,
      description,
      imageUrl
    })
  }
</script>

<form on:submit|preventDefault={submitForm}>
  <TextInput 
    id="title"
    label="Title"
    value={title}
    on:input={e => (title = e.target.value)} />
  <TextInput
    id="subtitle"
    label="Subtitle"
    value={subtitle}
    on:input={e => (subtitle = e.target.value)} />
  <TextInput 
    id="address" 
    label="Address"
    value={address}
    on:input={e => (address = e.target.value)} />
  <TextInput 
    id="image" 
    label="Image URL"
    value={imageUrl}
    on:input={e => (imageUrl = e.target.value)} />
  <TextInput 
    id="email" 
    label="E-Mail"
    value={email}
    on:input={e => (email = e.target.value)} />
  <TextInput
    controlType="textArea"
    rows=3
    id="description" 
    label="Description"
    type="email"
    value={description}
    on:input={e => (description = e.target.value)} />
  <Button type="submit" caption="Save" />
</form>

<style>
  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>