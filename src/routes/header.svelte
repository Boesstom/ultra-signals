<!-- src/routes/header.svelte -->
<script>
    import { page } from '$app/stores';
</script>
<header class="bg-white shadow-sm">
    <div class="container mx-auto px-6 py-4 flex items-center">
        <!-- Logo -->
        <div class="flex items-center">
            <a href="/" class="flex items-center">
                <img src="/ultra-logo-black.png" alt="Ultra Signals" class="h-8" />
            </a>
        </div>

        <!-- Main Navigation -->
        <nav class="hidden md:flex space-x-8 items-center ml-8">
            <a href="/" class="relative p-2 rounded-lg group hover:bg-gradient-to-r from-[#FF6B6B] to-[#4ECDC4] hover:p-[2px]" aria-current={$page.url.pathname === "/" ? "page" : undefined}>
                <span class="flex items-center text-gray-800 hover:text-gray-600 font-medium bg-white rounded-lg p-2">Home</span>
            </a>
            <a href="/ultra-1-pass" class="relative p-2 rounded-lg group hover:bg-gradient-to-r from-[#FF6B6B] to-[#4ECDC4] hover:p-[2px]" aria-current={$page.url.pathname === "/ultra-1-pass" ? "page" : undefined}>
                <span class="flex items-center bg-white rounded-lg p-2">
                    <img src="/ultra1pass.svg" alt="Ultra 1 Pass" class="h-3" />
                </span>
            </a>
            <a href="/ultra-2-pass" class="relative p-2 rounded-lg group hover:bg-gradient-to-r from-[#FF6B6B] to-[#4ECDC4] hover:p-[2px]" aria-current={$page.url.pathname === "/ultra-2-pass" ? "page" : undefined}>
                <span class="flex items-center bg-white rounded-lg p-2">
                    <img src="/ultra2pass.svg" alt="Ultra 2 Pass" class="h-3" />
                </span>
            </a>
        </nav>

        <!-- Push right navigation to the end -->
        <div class="flex-1 flex justify-end">
            <div class="flex items-center space-x-6">
                <a href="/keygen" class="flex items-center text-gray-800 hover:text-gray-600 font-medium">
                    <span class="flex items-center">
                        <span class="rainbow-border p-[1px] rounded-md mr-2 flex items-center justify-center">
                            <img src="/key-logo.svg" alt="Key Logo" class="h-5" />
                        </span>
                        <span>Keygen Distribution Entry</span>
                    </span>
                </a>
                <a href="/faq" class="text-gray-800 hover:text-gray-600 font-medium">FAQ</a>
                <a href="/contact" class="text-gray-800 hover:text-gray-600 font-medium">Contact</a>
            </div>
        </div>
    </div>
</header>