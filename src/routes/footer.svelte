<!-- src/routes/footer.svelte -->
<footer class="bg-black text-white py-12">
    <div class="container mx-auto px-1 flex flex-col">
        <div class="flex justify-between items-start">
            <!-- Kontak -->
            <div class="space-y-4">
                <p class="text-sm flex items-center gap-2">
                    <img src="/contact-us-session.svg" alt="Sessions" class="w-[15px] h-[17px]" />
                    <span class="font-medium font-poppins text-[14px]">Contact us on Sessions</span>
                </p>
                <h2 class="text-[32px] font-medium font-poppins max-w-[700px]">
                    Any questions regarding a signal <span class="font-normal text-[#C8C8C8]">that we have distributed or our data brokerage intelligence solicitation?</span>
                </h2>
                <button class="rainbow-button text-white px-6 py-2 rounded-md font-bold">
                    CONTACT US &rarr;
                </button>
            </div>
    
            <!-- Logo -->
            <img src="/ultra-logo-white.png" alt="Ultra Signals Network" class="h-12" />
        </div>
        
        <!-- Navigation -->
        <nav class="mt-8 flex gap-8 items-center justify-end">
            <a href="#home" class="text-gray-400 hover:text-white">Home</a>
            <a href="#ultra1" class="text-gray-400 hover:text-white group flex items-center">
                <img src="/ultra1passwhite.svg" alt="Ultra 1 Pass" class="h-3 opacity-70 transition-opacity duration-200 group-hover:opacity-100" />
            </a>
            <a href="#ultra2" class="text-gray-400 hover:text-white group flex items-center">
                <img src="/ultra2passwhite.svg" alt="Ultra 2 Pass" class="h-3 opacity-70 transition-opacity duration-200 group-hover:opacity-100" />
            </a>
            <a href="#keygen" class="text-gray-400 hover:text-white">Keygen Distribution Entry</a>
            <a href="#faq" class="text-gray-400 hover:text-white">FAQ</a>
            <a href="#contact" class="text-gray-400 hover:text-white">Contact</a>
        </nav>
    </div>

    <!-- Bottom Bar -->
    <div class="border-t border-gray-700 mt-8 pt-8">
        <div class="container mx-auto px-4 flex justify-between items-center">
            <div class="text-[14px] font-medium font-poppins bg-gradient-to-r from-blue-400 via-green-500 to-purple-500 bg-clip-text text-transparent">Ultra Signals. Validated Keygen Service.<br>Created by 0xScorpion & Staff</div>
            <div class="flex items-center gap-8">
                <img src="/keygen-logo-white.svg" alt="Ultra Logo" class="h-8" />
                <img src="/signature.png" alt="Signature" class="h-8" />
            </div>
        </div>
    </div>
</footer>