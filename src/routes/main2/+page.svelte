<script>
    import { goto } from "$app/navigation";
    import { onMount } from "svelte";

    let username;

    onMount(() => {
        if (!localStorage.hasOwnProperty('accessToken_google')) {
            alert('로그인을 해주세요.');
            goto('/');
        }
        getUserInfo_google()
    })

    const googleAPI = `https://www.googleapis.com/oauth2/v2/userinfo?access_token=${localStorage.getItem('accessToken_google')}`;

    const getUserInfo_google = () => {
        fetch(googleAPI,{
            method:'GET',
            headers: {
                authorization : `Bearer ${localStorage.getItem('accessToken_google')}`,
            },
        })
        .then((res) => { return res.status })
        .then((data) => {
            if (data == 200) console.log('ok')
        })
    }

</script>

{#if localStorage.hasOwnProperty('accessToken_google')}
    <h1>구글 로그인 Welcome~~</h1>
{:else}
    <a href="/">로그인해주세요!</a>
{/if}

<style>
    * {
        display: flex; 
        justify-content: center;
    }
</style>