<script>
	// import '../app.postcss';
    import Form from './form.svelte';
	import { Button, Navbar, NavBrand, NavLi, NavUl, NavHamburger, DarkMode, Avatar } from 'flowbite-svelte';
	import logo from '../lib/images/logo.svg';
    import avatar from '../lib/images/avatar.svg';
    let page = 0;
    function page0() {page = 0;}
    function page1() {page = 1;}

</script>

<Navbar let:hidden let:toggle>
	<NavBrand on:click={page0}>
		<img src={logo} class="mr-3 h-6 sm:h-9" alt="Flowbite Logo" />
		<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">Flowbite</span>
	</NavBrand>
    <DarkMode></DarkMode>

	<NavHamburger on:click={toggle} />
	<NavUl {hidden}>
		<NavLi class="cursor-pointer" on:click={page1}>Benchmark</NavLi>
        
	</NavUl>
    <Button>LeaderBoard</Button>
    <Avatar src="{avatar}" style="background-color:#111827;" rounded />
</Navbar>
<div>
	{#if page==0}
        <slot />
    {/if}
    {#if page==1}
        <From />
    {/if}
</div>

<style>
	div {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100vh;
		font-family: ubuntu;
	}
</style>
