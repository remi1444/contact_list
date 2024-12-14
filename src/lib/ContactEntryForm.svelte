<script>
        import { number, name, moreInfo, contactList } from "../../store/data";

        function addContact() {
                const uniqueID = crypto.randomUUID() + Math.random();
                const hex = Math.floor(Math.random() * 16777215).toString(16);
                const hexBg = Math.floor(Math.random() * 16777215).toString(16);
                const randomBgColor = `rgba(${parseInt(hexBg.slice(0, 2), 16)}, ${parseInt(hexBg.slice(2, 4), 16)}, ${parseInt(hexBg.slice(4, 6), 16)}, 0.4)`;

                const randomColor = `#${hex.padStart(6, "0")}`;
                contactList.update((currentList) => [
                        {
                                name: $name,
                                number: $number,
                                moreInfo: $moreInfo,
                                uniqueID,
                                randomColor,
                                randomBgColor
                        },
                        ...currentList
                ]);

                // console.log($contactList);
        }
</script>

<form
        on:submit={(e) => {
                e.preventDefault();
                if (
                        $name.length < 3 ||
                        ($name == "" && $number.length < 10) ||
                        ($number == "" && $moreInfo.length < 5) ||
                        $number == undefined
                ) {
                        return;
                }
                addContact();

                // $name = "";
                // $number = "";
                // $moreInfo = "";
        }}
>
        <div class="">
                <label for="name">Name</label>
                <input
                        type="text"
                        name="name"
                        id="name"
                        placeholder="'Tilumbu 😄'"
                        bind:value={$name}
                />
        </div>

        <div class="">
                <label for="number">Number</label>
                <input
                        type="number"
                        name="number"
                        minlength="3"
                        id="number"
                        placeholder="+234-8115-200-788"
                        bind:value={$number}
                />
        </div>

        <div class="">
                <label for="more_info">More Contact Info</label>
                <textarea
                        name="more_info"
                        id="more_info"
                        placeholder="E.G: This is my brother"
                        maxlength="20"
                        minlength="7"
                        bind:value={$moreInfo}
                ></textarea>
        </div>

        <button type="submit">Add New Contact</button>
</form>

<style>
        div {
                display: flex;
                flex-direction: column;
                margin-bottom: 1em;
        }
        label {
                text-align: left;
                font-weight: bold;
                color: rgba(37, 33, 33, 0.671);
                cursor: pointer;
        }
        input {
                padding: 0.6em 1em;
                border-radius: 3px;
                cursor: pointer;
        }
        textarea {
                padding: 1em 1em;
                border-radius: 3px;
                cursor: pointer;
                border: 2px solid black;
        }
        button {
                background: green;
                color: aliceblue;
                padding: 0.4em 3em;
                cursor: pointer;
        }
</style>
