<script lang="ts">
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	let mobileMenuOpen = $state(false);
	let mounted = $state(false);

	onMount(() => {
		mounted = true;
	});

	const navItems = [
		{ href: '/', label: 'Home', icon: 'home' },
		{ href: '/about', label: 'About', icon: 'user' },
		{ href: '/services', label: 'Services', icon: 'briefcase' },
		{ href: '/contact', label: 'Contact', icon: 'mail' }
	];

	function toggleMobileMenu() {
		mobileMenuOpen = !mobileMenuOpen;
	}

	function handleMobileNavClick(event: MouseEvent, href: string) {
		event.preventDefault();
		mobileMenuOpen = false;
		goto(href);
	}
</script>

<nav class="bg-gray-50 border-b border-gray-200">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex justify-between items-center h-16">
			<!-- Logo/Brand -->
			<div class="flex-shrink-0">
				<a href="/" class="text-xl font-semibold text-gray-800">Site</a>
			</div>

			<!-- Desktop Navigation -->
			<div class="hidden md:flex md:space-x-8">
				{#each navItems as item}
					<a
						href={item.href}
						class="flex items-center space-x-2 px-3 py-2 text-sm font-medium transition-colors {$page
							.url?.pathname === item.href
							? 'text-gray-900 border-b-2 border-gray-900'
							: 'text-gray-600 hover:text-gray-900'}"
					>
						{#if item.icon === 'home'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
								></path>
							</svg>
						{:else if item.icon === 'user'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
								></path>
							</svg>
						{:else if item.icon === 'briefcase'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
								></path>
							</svg>
						{:else if item.icon === 'mail'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
								></path>
							</svg>
						{/if}
						<span>{item.label}</span>
					</a>
				{/each}
			</div>

			<!-- Mobile menu button -->
			<div class="md:hidden">
				<button
					type="button"
					onclick={toggleMobileMenu}
					class="inline-flex items-center justify-center p-2 rounded-md text-gray-600 hover:text-gray-900 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-gray-500"
					aria-expanded="false"
				>
					<span class="sr-only">Open main menu</span>
					{#if mobileMenuOpen}
						<svg
							class="w-6 h-6"
							fill="none"
							stroke="currentColor"
							viewBox="0 0 24 24"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M6 18L18 6M6 6l12 12"
							></path>
						</svg>
					{:else}
						<svg
							class="w-6 h-6"
							fill="none"
							stroke="currentColor"
							viewBox="0 0 24 24"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M4 6h16M4 12h16M4 18h16"
							></path>
						</svg>
					{/if}
				</button>
			</div>
		</div>
	</div>

	<!-- Mobile Navigation -->
	{#if mobileMenuOpen && mounted}
		<div class="md:hidden border-t border-gray-200">
			<div class="px-2 pt-2 pb-3 space-y-1">
				{#each navItems as item}
					<a
						href={item.href}
						onclick={(e) => handleMobileNavClick(e, item.href)}
						class="flex items-center space-x-3 px-3 py-2 text-base font-medium rounded-md transition-colors {$page
							.url?.pathname === item.href
							? 'bg-gray-100 text-gray-900'
							: 'text-gray-600 hover:bg-gray-50 hover:text-gray-900'}"
					>
						{#if item.icon === 'home'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
								></path>
							</svg>
						{:else if item.icon === 'user'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
								></path>
							</svg>
						{:else if item.icon === 'briefcase'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
								></path>
							</svg>
						{:else if item.icon === 'mail'}
							<svg
								class="w-5 h-5"
								fill="none"
								stroke="currentColor"
								viewBox="0 0 24 24"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
								></path>
							</svg>
						{/if}
						<span>{item.label}</span>
					</a>
				{/each}
			</div>
		</div>
	{/if}
</nav>
