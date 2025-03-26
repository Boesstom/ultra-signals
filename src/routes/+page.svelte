<!-- src/routes/+page.svelte -->
<script>
    import '../app.css';
    import Header from './header.svelte';
    import Footer from './footer.svelte';
    import KeygenPortal from './keygen-portal.svelte';
    import { page } from '$app/stores';
</script>

<Header />
<KeygenPortal />
<Footer />

<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        background: white;
    }
</style>