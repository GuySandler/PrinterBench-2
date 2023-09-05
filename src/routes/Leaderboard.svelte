<script>
    import { Heading, P, Button } from 'flowbite-svelte';
    import { PUBLIC_VITE_FIREKEY } from '$env/static/public';
    import { getFirestore } from 'firebase/firestore';
    import { initializeApp } from "firebase/app";
    import { getAnalytics } from "firebase/analytics";
    const firebaseConfig = {
        apiKey: PUBLIC_VITE_FIREKEY,
        authDomain: "printerbench2.firebaseapp.com",
        projectId: "printerbench2",
        storageBucket: "printerbench2.appspot.com",
        messagingSenderId: "661761044534",
        appId: "1:661761044534:web:c84431d35b5c8db35ba897",
        measurementId: "G-L67B7KZEYH"
    };
    const app = initializeApp(firebaseConfig);
    const analytics = getAnalytics(app);
    const db = getFirestore();
</script>
<center>
    <Heading tag="h2">Leaderboard</Heading>
    <Heading tag="h4">Click on a printer!</Heading>
    <div class="top1">

    </div>
    <div class="top2">
        
    </div>
    <div class="top3">
        
    </div>
    <div class="top4">
        
    </div>
    <div class="top4">
        
    </div>
    <div class="top4">
        
    </div>
    <div class="top4">
        
    </div>
    <div class="top4">
        
    </div>
    <div class="top4">
        
    </div>
    <div class="top4">
        
    </div>
</center>
<style>
    .top1 {
        width:55vw;
        height:50px;
        background-color:rgb(230,169,26);
        border-radius:7.5px;
        border:1px solid black;
        margin-top:7.5px;
        margin-bottom:7.5px;
    }
    .top2 {
        width:55vw;
        height:50px;
        background-color:#7D7D7D;
        border-radius:7.5px;
        border:1px solid black;
        margin-top:7.5px;
        margin-bottom:7.5px;
    }
    .top3 {
        width:55vw;
        height:50px;
        background-color:#A77A38;
        border-radius:7.5px;
        border:1px solid black;
        margin-top:7.5px;
        margin-bottom:7.5px;
    }
    .top4 {
        width:55vw;
        height:50px;
        background-color:#60B8C7;
        border-radius:7.5px;
        border:1px solid black;
        margin-top:7.5px;
        margin-bottom:7.5px;
    }
</style>