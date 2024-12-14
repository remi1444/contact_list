<script>
        import ContactData from "./ContactData.svelte";
        import ContactEntryForm from "./ContactEntryForm.svelte";
        import Header from "./Header.svelte";
</script>

<div class="">
        <Header />
        <ContactEntryForm />
        <ContactData />
</div>

<style>
        div {
                display: flex;
                overflow: hidden;
                max-width: 900px;
                /* min-width: 600px; */
                flex-direction: column;
                width: 100%;
                /* border: 2px solid rgb(199, 179, 245); */
        }
</style>
