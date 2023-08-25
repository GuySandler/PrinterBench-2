<script>
	import '../app.postcss';
	import { Button, Navbar, NavBrand, NavLi, NavUl, NavHamburger, DarkMode, Avatar } from 'flowbite-svelte';
	import logo from '../lib/images/logo.svg';
    import avatar from '../lib/images/avatar.svg';
</script>

<Navbar let:hidden let:toggle>
	<NavBrand href="/">
		<img src={logo} class="mr-3 h-6 sm:h-9" alt="Flowbite Logo" />
		<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">Flowbite</span
		>
        <DarkMode style="margin-left:10px;"></DarkMode>
	</NavBrand>
    
	<NavHamburger on:click={toggle} />
	<NavUl {hidden}>
		<NavLi href="/">Home</NavLi>
		<NavLi href="/about">About</NavLi>
		<NavLi href="/docs/components/navbar">Navbar</NavLi>
        
	</NavUl>
    <Button>LeaderBoard</Button>
    <Avatar src="{avatar}" style="background-color:#111827;" rounded />
</Navbar>
<div>
	<slot />
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
