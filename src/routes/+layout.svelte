<script>
	import '../app.postcss';
    import Form from './Form.svelte';
    import LeaderBoard from './Leaderboard.svelte';
	import { Rating, Button, Navbar, NavBrand, NavLi, NavUl, NavHamburger, DarkMode, Avatar } from 'flowbite-svelte';
	import logo from '../lib/images/logo.svg';
    import avatar from '../lib/images/avatar.svg';
	import Leaderboard from './Leaderboard.svelte';
    let page = 0;
    function page0() {page = 0;}
    function page1() {page = 1;}
    function page2() {page = 2;}
</script>

<Navbar style="margin-bottom:1%;" let:hidden let:toggle>
	<button on:click={page0}>
        <NavBrand>
                <img src={logo} class="mr-3 h-6 sm:h-9" alt="Flowbite Logo" />
                <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">Flowbite</span>
        </NavBrand>
    </button>
    <DarkMode></DarkMode>

	<NavHamburger on:click={toggle} />
	<NavUl {hidden}>
		<NavLi class="cursor-pointer" on:click={page1}>Benchmark</NavLi>
        
	</NavUl>
    <Button on:click={page2}>LeaderBoard</Button>
    <Avatar src="{avatar}" style="background-color:#111827;" rounded />
</Navbar>
<div>
	{#if page==0}
        <slot />
    {:else if page==1}
        <Form />
    {:else if page==2}
        <Leaderboard />
    {:else}
        <h1>ERROR: Page not found</h1>
    {/if}
</div>

<style>
	div {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100%;
		font-family: ubuntu;
	}
</style>
