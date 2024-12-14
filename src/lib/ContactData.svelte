<script>
        import { contactList } from "../../store/data";
        import { Frown } from "lucide-svelte";

        let editingContact = null; 
        let editedName = "";
        let editedNumber = "";
        let editedMoreInfo = "";

        
        function editContact(contact) {

            console.log(contact);
            
                editingContact = contact;
                editedName = contact.name;
                editedNumber = contact.number;
                editedMoreInfo = contact.moreInfo;
        }

    
        function saveContact() {
                if (editingContact) {
                        editingContact.name = editedName;
                        editingContact.number = editedNumber;
                        editingContact.moreInfo = editedMoreInfo;
                        contactList.update((contacts) => [...contacts]);
                        editingContact = null;
                }
        }

        function deleteContact(contact) {
                console.log({ contact });

                contactList.update((contacts) => contacts.filter((c) => c !== contact));
        }
</script>

<section class="">
        {#if $contactList.length < 1}
                <div class="pulse">
                        <p>No contact saved!</p>
                        <Frown />
                </div>
        {:else}
                {#each $contactList as contactDetails}
                        <div class="card" style="background: {contactDetails.randomBgColor};">
                                <div class="details">
                                        <p
                                                class="avatar"
                                                style="background: {contactDetails.randomColor};"
                                        >
                                                {contactDetails.name[0]?.toUpperCase()}
                                        </p>
                                        <p class="name">{contactDetails.name}</p>
                                        <p class="number">{contactDetails.number}</p>
                                        <p class="info">{contactDetails.moreInfo}</p>
                                </div>

                                <div>
                                        <button on:click={() => editContact(contactDetails)}
                                                >Edit</button
                                        >
                                        <button on:click={() => deleteContact(contactDetails)}
                                                >Delete</button
                                        >
                                </div>
                        </div>
                {/each}
        {/if}

        {#if editingContact}
                <div class="modal_blur">
                        <div class="edit-form">
                                <h3>Edit Contact</h3>
                                <form on:submit|preventDefault={saveContact}>
                                        <div>
                                                <label for="name">Name</label>
                                                <input
                                                        id="name"
                                                        bind:value={editedName}
                                                        placeholder="Edit name"
                                                />
                                        </div>
                                        <div>
                                                <label for="number">Number</label>
                                                <input
                                                        id="number"
                                                        bind:value={editedNumber}
                                                        placeholder="Edit number"
                                                />
                                        </div>
                                        <div>
                                                <label for="moreInfo">More Info</label>
                                                <input
                                                        id="moreInfo"
                                                        bind:value={editedMoreInfo}
                                                        placeholder="Edit more info"
                                                />
                                        </div>
                                        <button type="submit">Save</button>
                                        <button
                                                type="button"
                                                on:click={() => (editingContact = null)}
                                                >Cancel</button
                                        >
                                </form>
                        </div>
                </div>
        {/if}
</section>

<style>
        .modal_blur {
                height: 100vh;
                width: 100vw;
                background: rgba(0, 0, 0, 0.9);
                position: fixed;
                top: 0%;
                left: 0%;
                width: 100%;
                display: flex;
                justify-content: center;
                align-items: center;
        }
        .edit-form {
                margin-top: 2em;
                padding: 1em;
                background-color: #f4f4f4;
                border-radius: 7px;
                width: 85%;
                max-width: 500px;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
        }

        .edit-form input {
                margin: 0.5em 0;
                padding: 0.6em;
                width: 90%;
                border-radius: 5px;
                
        }

        .edit-form button {
                margin-top: 1em;
                padding: 0.5em;
                background-color: #4caf50;
                color: white;
                border: none;
                cursor: pointer;
        }

        .edit-form button[type="button"] {
                background-color: #f44336;
        }
        /* Apply the pulsing effect to a class */
        .pulse {
                display: inline-block; /* Makes it work well with inline elements like text */
                animation: pulse 1.5s infinite; /* Apply the pulse animation */
                animation-timing-function: ease-in-out; /* Smooth transition */
        }

        @keyframes pulse {
                0% {
                        transform: scale(1);
                        opacity: 1;
                }
                50% {
                        transform: scale(1.1); /* Slightly enlarge the element */
                        opacity: 0.7; /* Slightly reduce the opacity */
                }
                100% {
                        transform: scale(1);
                        opacity: 1;
                }
        }

        .details {
                display: flex;
                justify-content: space-evenly;
                border: 1px solid rgb(46, 48, 46);
                font-size: x-small;
        }
        .info {
                border-left: 1px solid rgb(10, 6, 14);
                border-right: 1px solid rgb(10, 6, 14);
                padding: 0 6px;
                width: 40%;
                text-align: left;
                margin-right: 4px;
                display: flex;
                justify-content: center;
                align-items: center;
        }
        .number {
                padding: 0 6px;
                display: flex;
                justify-content: center;
                align-items: center;
        }
        .name {
                border-left: 1px solid rgb(10, 6, 14);
                border-right: 1px solid rgb(10, 6, 14);
                padding: 0 6px;
                display: flex;
                justify-content: center;
                align-items: center;
        }
        .avatar {
        
                border-radius: 100%;
                color: white;
                height: 30px;
                width: 30px;
                min-width: 30px;
                margin-left: 0.4em;
                margin-right: 0.4em;
                display: flex;
                justify-content: center;
                align-items: center;
                font-size: larger;
                font-weight: bolder;
        }
        .card {
                border-radius: 3px;
                border: 1px solid rgb(46, 48, 46);
                margin: 0.4em 0;
                height: fit-content;
                padding: 1em;
                background-color: aqua;
        }
        section {
                background: rgba(56, 87, 15, 0.144);
                height: 350px;
                overflow-y: scroll;
                margin-top: 1em;
        }
        button {
                padding: 0.3em 1em;
                margin-top: 0.6em;
                font-size: small;
        }
        button:first-of-type {
                background: green;
                color: whitesmoke;
        }
        button:last-of-type {
                background: red;
                color: whitesmoke;
        }
</style>
