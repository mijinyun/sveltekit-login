<script>
    import { goto } from '$app/navigation';
    import { page } from '$app/stores';
    import { onMount } from 'svelte';
    
    const param = $page.url.search;

    onMount(() => {
        getToken()
    })

    const getToken = () => {
        const code = param.split('=').reverse()[0];
        
        const bodyData = {
            grant_type: "authorization_code",
            client_id : "19901113b9a9909609147a67ffc2a953",
            redirect_uri : "https://sveltekit-login.vercel.app/kakaologin",
            // redirect_uri : "http://localhost:5173/kakaologin",
            code : code
        }
        const queryStringBody = Object.keys(bodyData).map(key => encodeURIComponent(key) + "=" + encodeURI(bodyData[key])).join('&');

        fetch('https://kauth.kakao.com/oauth/token', {
        method:"POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded;charset=utf-8",
            "Authorization" : "Bearer"
        },
        body: queryStringBody
    })
    .then(res => res.json())
    .then((data) => { 
        localStorage.setItem('accessToken_kakao',data.access_token)
        goto('/main')
     })
    }
</script>