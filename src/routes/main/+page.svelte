<script>
    import { goto } from "$app/navigation";
    import { onMount } from "svelte";

    let username;

    onMount(() => {
        if (!localStorage.hasOwnProperty('accessToken_kakao')) {
            alert('로그인을 해주세요.');
            goto('/')
        }
        getUserInfo_kakao()
    })
    
    const getUserInfo_kakao = () => {
        fetch('https://kapi.kakao.com/v2/user/me',{
            method:"GET",
            headers: {
                "Content-Type" : "application/x-www-form-urlencoded;charset=utf-8",
                "Authorization" : "Bearer " + localStorage.getItem('accessToken_kakao')
            }
        })
        .then(res => res.json())
        .then((data) => {
            username = data.properties.nickname;
        })
        .catch(err => alert(err));
    }

</script>

{#if localStorage.hasOwnProperty('accessToken_kakao')}
    <h1>{username}(kakao)님 Welcome!!!</h1>
{:else}
    <a href="/">로그인해주세요!</a>
{/if}

<style>
    * {
        display: flex; 
        justify-content: center;
    }
</style>