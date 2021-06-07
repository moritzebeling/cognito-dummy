<script>

    import Amplify, { Auth } from 'aws-amplify';

    Amplify.configure({
        Auth: {

            // REQUIRED only for Federated Authentication - Amazon Cognito Identity Pool ID
            identityPoolId: 'eu-central-1:be559466-d17f-4f5f-85e6-b867927af67e',

            // REQUIRED - Amazon Cognito Region
            region: 'eu-central-1',

            // OPTIONAL - Amazon Cognito User Pool ID
            userPoolId: 'eu-central-1_InrFTmbei',

            // OPTIONAL - Amazon Cognito Web Client ID (26-char alphanumeric string)
            userPoolWebClientId: '2mmpk4rria1jdsgoeg9l73csnk',

            // OPTIONAL - Configuration for cookie storage
            // Note: if the secure flag is set to true, then the cookie transmission requires a secure protocol
            cookieStorage: {
                // REQUIRED - Cookie domain (only required if cookieStorage is provided)
                domain: '.yourdomain.com',
                // OPTIONAL - Cookie path
                path: '/',
                // OPTIONAL - Cookie expiration in days
                expires: 365,
                // OPTIONAL - See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite
                sameSite: "strict",
                // OPTIONAL - Cookie secure flag
                // Either true or false, indicating if the cookie transmission requires a secure protocol (https).
                secure: true
            },

        }
    });

    import Navigation from '$lib/Navigation.svelte';

</script>

<Navigation />

<slot />
