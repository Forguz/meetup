<script>
  import Header from './UI/Header.svelte';
  import MeetupGrid from './Meetups/MeetupGrid.svelte';
  import TextInput from './UI/TextInput.svelte';
  import Button from './UI/Button.svelte';

  let title = '';
  let subtitle = '';
  let address = '';
  let email = '';
  let description = '';
  let imageUrl = '';

  let meetups = [
    {
      id: 'm1',
      title: 'Coding Bootcamp',
      subtitle: 'Learn to code in 2 hours',
      description: 'In this meetup, we will have some experts that teach you how to code',
      imageUrl: 'https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fupload.wikimedia.org%2Fwikipedia%2Fcommons%2Fthumb%2F8%2F8d%2FMoirans_(38)_tour.jpg%2F1200px-Moirans_(38)_tour.jpg&f=1&nofb=1',
      address: '27th Nerd Road, 32523 New York',
      contactEmail: 'code@test.com',
      isFavorite: false
    },
    {
      id: 'm2',
      title: 'Swim Together',
      subtitle: 'Let\'s go for some swimming',
      description: 'We will simply swim some rounds',
      imageUrl: 'https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fupload.wikimedia.org%2Fwikipedia%2Fcommons%2Fthumb%2F8%2F8d%2FMoirans_(38)_tour.jpg%2F1200px-Moirans_(38)_tour.jpg&f=1&nofb=1',
      address: '27th Nerd Road, 32523 New York',
      contactEmail: 'swim@test.com',
      isFavorite: false
    }
  ];

  function addMeetup() {
    const newMeetup = {
      id: Math.random().toString(),
      title,
      subtitle,
      description,
      imageUrl,
      address,
      contactEmail: email
    }

    meetups = [newMeetup, ...meetups]
  }

  function toggleFavorite(event) {
    const id = event.detail;
    const updatedMeetup = { ...meetups.find(meetup => meetup.id === id) };
    updatedMeetup.isFavorite = !updatedMeetup.isFavorite;

    const meetupIndex = meetups.findIndex(meetup => meetup.id === id);
    const updatedMeetups = [...meetups];
    updatedMeetups[meetupIndex] = updatedMeetup;

    meetups = updatedMeetups;
  }
</script>

<Header />
<main>
  <form on:submit|preventDefault={addMeetup}>
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
  <MeetupGrid {meetups} on:togglefavorite={toggleFavorite}/>
</main>

<style>
  main {
    margin-top: 5rem;
  }

  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>