<script>
    import { goto } from '$app/navigation';
    import { page } from '$app/stores';
    import { onMount } from 'svelte';

    let url = $page.url.hash;
    let accessToken_google = url.split('&')[0].split('=')[1];

    onMount(() => {
        localStorage.setItem('accessToken_google',accessToken_google);
        if (localStorage.hasOwnProperty('accessToken_google')) {
        goto('/main2')
    }
    })

</script>