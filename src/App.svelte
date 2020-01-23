<script>
  let name = "";
  let contact = "";
  let contactList = [];

  const contactSave = event => {
    event.preventDefault();
    if (name !== "" && contact !== "") {
      contactList = [
        {
          name,
          contact
        },
        ...contactList
      ];

	  console.log(contactList);
	  name = '';
	  contact = '';
    }
  };

  const removeCard = no => {
	let newContactList = []
	let newCard;
	console.log(no);
	contactList = contactList.map(item =>{
		if(item.contact !== no){
			return item
		}
		return {}
	})
	console.log(contactList)

	// console.log(newContactList)
  }
</script>

<style>
  .mycontainer {
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    align-content: flex-start;
    width: 30%;
  }
  .card {
    width: 100%;
  }

</style>

<div class="container m-auto mycontainer">
  <div class="card mt-5">
    <div class="card-header">Contact Form</div>
    <div class="card-body">
      <form>
        <div class="form-group">
          <label for="exampleInputEmail1">Name</label>
          <input
            type="name"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
            bind:value={name} />
        </div>
        <div class="form-group">
          <label for="exampleInputPassword1">Contact No.</label>
          <input
            type="contact"
            class="form-control"
            id="exampleInputPassword1"
            bind:value={contact} />
        </div>
        <button type="submit" class="btn btn-primary" on:click={contactSave}>
          Save
        </button>
      </form>
    </div>
  </div>
</div>
<hr />
<div class="container">
<div class="row mb-2">
  {#if contactList.length > 0}
    {#each contactList as card (card.contact)}
    {#if card.name && card.contact}
	<div class="col-sm-12 col-md-4 mb-2">    
        <div class="card">
          <div class="card-body">
            <h3>{card.name}</h3>
            <h4>{card.contact}</h4>
            <div class="text-right">
              <button
                type="button"
                class="btn btn-danger"
                on:click={removeCard.bind(this, card.contact)}>
                Danger
              </button>
            </div>
          </div>
        </div>
	  </div>
     {/if}
    {/each}
  {:else}
    <p>add some cards....</p>
  {/if}
</div>
</div>
