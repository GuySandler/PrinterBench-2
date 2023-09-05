<script>
    import { Textarea, Label, Input, Select, Button, Toggle, A } from 'flowbite-svelte';
    import { Icon } from 'flowbite-svelte-icons';
    import Rating from './rating.svelte';
    import { starss } from './stores.js';
    import { PUBLIC_VITE_FIREKEY } from '$env/static/public';
    import { initializeApp } from "firebase/app";
    import { getAnalytics } from "firebase/analytics";
    import { getFirestore, addDoc, collection, getDocs, doc, setDoc } from 'firebase/firestore';
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

    let star = null;
	starss.subscribe((value) => {
		star = value;
	});

    let types = [
        { value: 'bed', name: 'Bedslinger' },
        { value: 'core', name: 'Core XY' },
        { value: 'delta', name: 'Delta' }
    ];
    let firmweres = [
        { value: 'klip', name: 'Klipper' },
        { value: 'mar', name: 'Marlin' },
        { value: 'oth', name: 'Other' }
    ]

    let form = [
        { value: 'name', name: '' },
        { value: 'comp', name: '' },
        { value: 'cost', name: 1 },
        { value: 'type', name: '' },
        { value: 'firm', name: '' },
        { value: 'xmm', name: 1 },
        { value: 'ymm', name: 1 },
        { value: 'zmm', name: 1 },
        { value: 'hmm', name: 1 },
        { value: 'diam', name: 1 },
        { value: 'flow', name: 1 },
        { value: 'cost', name: 1 },
        { value: 'comment', name: ''}
    ]
    let Features = [
        { value: 'FS', name: false },
        { value: 'Enc', name: false },
        { value: 'Cam', name: false },
        { value: 'IS', name: false },
        { value: 'ABL', name: false },
        { value: 'OS', name: false },
        { value: 'AFL', name: false },
        { value: 'MC', name: false },
        { value: 'CS', name: false },
        { value: 'DD', name: false }
    ]
    let submited = false;
    function submitF() {
        if (form.name == '' || form.comp == '' ||
         form.cost == '' || form.type == '' ||
          form.firm == '' || form.flow == '' || 
          star == null) {
            if (form.type == 'delta') {
                if (form.diam == '' || form.hmm == '') {
                    alert('Please fill all the fields');
                }
            } else {
                if (form.xmm == '' || form.ymm == '' || form.zmm == '') {
                    alert('Please fill all the fields');
                }
            }
            alert('Please fill all the fields');
        } else {
            submited = true;
            Upload();
        }
    }
    function Upload() {
        addDoc(collection(db, "review"), {
            name: form.name,
            company: form.comp,
            cost: form.cost,
            type: form.type,
            firmware: form.firm,
            x: form.xmm,
            y: form.ymm,
            z: form.zmm,
            h: form.hmm,
            d: form.diam,
            flow: form.flow,
            comment: form.comment,
            stars: star,
            FS: Features.FS,
            Enc: Features.Enc,
            Cam: Features.Cam,
            IS: Features.IS,
            ABL: Features.ABL,
            OS: Features.OS,
            AFL: Features.AFL,
            MC: Features.MC,
            CS: Features.CS,
            DD: Features.DD
        })
    }
</script>
<div>
    <!-- <h1>{}</h1> -->
    <center>
        {#if !submited}
            <div class="sameline mb-6">
                <Input bind:value={form.name} id="name" placeholder="Name Of Printer" />
            </div>
            <div class="sameline mb-6">
                <Input bind:value={form.comp} id="company" placeholder="Company" />
            </div>
            <div class="sameline mb-6">
                <Input min="1" type="number" bind:value={form.cost} id="cost" placeholder="Cost">
                    <Icon name="dollar-solid" slot="left" class="w-5 h-5 text-gray-500 dark:text-gray-400" />
                </Input>
            </div>
            <Label>
                <div class="sameline">
                    Printer Type
                    <Select bind:value={form.type} class="cursor-pointer sameline mt-2 w-75" items={types} />
                </div>
                <div class="sameline">
                    Firmware
                    <Select bind:value={form.firm} class="cursor-pointer sameline mt-2 w-75" items={firmweres} />
                </div>
            </Label>
            <br>
            <Label>
                Build Volume
                <br>
                {#if form.type == 'delta'}
                    <div class="sameline mb-6" style="margin-top:10px;">
                        <Input min="1" type="number" bind:value={form.diam} id="diam" class="w-40" placeholder="Diameter" />
                    </div>
                    <div class="sameline mb-6">
                        <Input min="1" type="number" bind:value={form.hmm} id="zmm" class="w-40" placeholder="Hightmm" />
                    </div>
                {/if}
                {#if form.type != 'delta'}
                    <div class="sameline mb-6" style="margin-top:10px;">
                        <Input min="1" type="number" bind:value={form.xmm} id="xmm" class="w-40" placeholder="xmm" />
                    </div>
                    <div class="sameline mb-6">
                        <Input min="1" type="number" bind:value={form.ymm} id="ymm" class="w-40" placeholder="ymm" />
                    </div>
                    <div class="sameline mb-6">
                        <Input min="1" type="number" bind:value={form.zmm} id="zmm" class="w-40" placeholder="zmm" />
                    </div>
                {/if}
                <div class="mb-6">
                    <Input min="1" type="number" bind:value={form.flow} id="flow" class="w-40" placeholder="printing speed (mm)" />
                </div>
            </Label>
            <br>
            <div class="relative inline-flex items-center">
                <Label>
                    Features
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:checked={Features.FS} class="cursor-pointer sameline">Filament Sensor</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:checked={Features.Enc} class="cursor-pointer mt-3 sameline">Enclosure</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:checked={Features.Cam} class="cursor-pointer mt-3 sameline">Camera</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:checked={Features.IS} class="cursor-pointer mt-3">Input Shaping</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:checked={Features.ABL} class="cursor-pointer mt-3">Auto Bed Leveling</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:checked={Features.OS} class="cursor-pointer mt-3">Open Source</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:checked={Features.AFL} class="cursor-pointer mt-3">Auto First Layer</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:checked={Features.MC} class="cursor-pointer mt-3">Multicolor</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:checked={Features.CS} class="cursor-pointer mt-3">Cloud Services/Remote Access</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:checked={Features.DD} class="cursor-pointer mt-3">Direct Drive</Toggle>
                    </div>
                </Label>
            </div>
            <br>
            <Label>
                Star Rating
                <Rating />
            </Label>
            <br>
            <Label>
                <Textarea bind:value={form.comment} class="w-1/2" placeholder="Other comments (problems, special features)" rows="4" />
            </Label>
            <Button on:click={submitF} style="margin-top:20px;margin-bottom:50px;">Submit</Button>
        {/if}
        {#if submited}
            <h1>Thank You For Submitting</h1>
        {/if}
    </center>
</div>
<style>
    .sameline {
        display: inline-block;
        margin-left: 10px;
        margin-right: 10px;
    }
    
</style>