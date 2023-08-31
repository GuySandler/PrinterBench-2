<script>
    import { Rating, AdvancedRating, ScoreRating, Textarea, Label, Input, Select, Button, Toggle, A } from 'flowbite-svelte';

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
        { value: 'cost', name: 1 }
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
          form.firm == '' || form.xmm == '' ||
           form.ymm == '' || form.zmm == '' ||
            form.flow == '') {
            alert('Please fill all the fields');
        } else {
            submited = true;
            alert("Submitted")
        }
    }
</script>
<div>
    <center>
        {#if !submited}
            <div class="sameline mb-6">
                <Input bind:value={form.name} id="name" placeholder="Name Of Printer" />
            </div>
            <div class="sameline mb-6">
                <Input bind:value={form.comp} id="company" placeholder="Company" />
            </div>
            <div class="sameline mb-6">
                <Input bind:value={form.cost} id="cost" placeholder="Cost" />
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
                        <Input type="number" bind:value={form.diam} id="diam" class="w-40" placeholder="Diameter" />
                    </div>
                    <div class="sameline mb-6">
                        <Input type="number" bind:value={form.hmm} id="zmm" class="w-40" placeholder="Hightmm" />
                    </div>
                {/if}
                {#if form.type != 'delta'}
                <div class="sameline mb-6" style="margin-top:10px;">
                    <Input type="number" bind:value={form.xmm} id="xmm" class="w-40" placeholder="xmm" />
                </div>
                <div class="sameline mb-6">
                    <Input type="number" bind:value={form.ymm} id="ymm" class="w-40" placeholder="ymm" />
                </div>
                <div class="sameline mb-6">
                    <Input type="number" bind:value={form.zmm} id="zmm" class="w-40" placeholder="zmm" />
                </div>
                {/if}
                <div class="mb-6">
                    <Input type="number" bind:value={form.flow} id="flow" class="w-40" placeholder="flow mm" />
                </div>
            </Label>
            <br>
            <div class="relative inline-flex items-center">
                <Label>
                    Features
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:value={form.FS} class="cursor-pointer sameline">Filament Sensor</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:value={form.Enc} class="cursor-pointer mt-3 sameline">Enclosure</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:value={form.Cam} class="cursor-pointer mt-3 sameline">Camera</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:value={form.IS} class="cursor-pointer mt-3">Input Shaping</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:value={form.ABL} class="cursor-pointer mt-3">Auto Bed Leveling</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:value={form.OS} class="cursor-pointer mt-3">Open Source</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:value={form.AFL} class="cursor-pointer mt-3">Auto First Layer</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:value={form.MC} class="cursor-pointer mt-3">Multicolor</Toggle>
                    </div>
                    <br>
                    <div class="left sameline mb-6">
                        <Toggle bind:value={form.CS} class="cursor-pointer mt-3">Cloud Services/Remote Access</Toggle>
                    </div>
                    <div class="right sameline mb-6">
                        <Toggle bind:value={form.DD} class="cursor-pointer mt-3">Direct Drive</Toggle>
                    </div>
                </Label>
            </div>
            <br>
            <Label>
                <Textarea class="w-1/2" placeholder="Other comments (problems, special features)" rows="4" />
            </Label>
            <br>
            <Button on:click={submitF} style="margin-top:20px;">Submit</Button>
        {/if}
        {#if submited}
            <h1>Thank You For Submitting</h1>
        {/if}
        <slot/>
    </center>
</div>
<style>
    .sameline {
        display: inline-block;
        margin-left: 10px;
        margin-right: 10px;
    }
    
</style>