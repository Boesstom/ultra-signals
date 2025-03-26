<script>
  import { onMount } from 'svelte';

  let searchInput;
  let searchArrow;
  let dynamicPlaceholder;

  onMount(() => {
    const searchInput = document.getElementById('searchInput');
    const searchArrow = document.getElementById('searchArrow');
    const dynamicPlaceholder = document.getElementById('dynamicPlaceholder');
    const placeholder = searchInput.getAttribute('data-placeholder');
    
    // Format raw digits with hyphens
    function formatCode(digits) {
      let formatted = '';
      for (let i = 0; i < digits.length; i++) {
        // Add hyphen after 5th and 10th digit
        if (i === 5 || i === 10) {
          formatted += '-';
        }
        formatted += digits[i];
      }
      return formatted;
    }
    
    // Extract digits only from input value
    function extractDigits(value) {
      return value.replace(/[^0-9]/g, '').substring(0, 15);
    }
    
    // Update the visible input and placeholder
    function updateDisplay() {
      // Get only digits, limited to 15
      const rawDigits = extractDigits(searchInput.value);
      
      // Format with hyphens
      const formattedValue = formatCode(rawDigits);
      
      // Update input value with proper formatting
      searchInput.value = formattedValue;
      
      // Create a placeholder that shows format but hides typed characters
      const formattedPlaceholder = 'XXXXX-XXXXX-XXXXX';
      let updatedPlaceholder = '';
      
      if (formattedValue.length > 0) {
        // For each character in the placeholder format
        for (let i = 0; i < formattedPlaceholder.length; i++) {
          if (i < formattedValue.length) {
            // Make placeholder character invisible where user has typed
            updatedPlaceholder += '<span style="opacity: 0;">' + formattedPlaceholder[i] + '</span>';
          } else {
            // Show remaining placeholder characters
            updatedPlaceholder += formattedPlaceholder[i];
          }
        }
      } else {
        updatedPlaceholder = formattedPlaceholder;
      }
      
      dynamicPlaceholder.innerHTML = updatedPlaceholder;
    }
    
    // Handle input changes
    searchInput.addEventListener('input', function(e) {
      updateDisplay();
    });
    
    // Handle pasting
    searchInput.addEventListener('paste', function(e) {
      // Let the paste happen, then format afterward
      setTimeout(updateDisplay, 0);
    });
    
    // Handle Enter key press
    searchInput.addEventListener('keypress', function(e) {
      if (e.key === 'Enter') {
        console.log('Search value:', searchInput.value);
        // You can extract just the digits if needed
        console.log('Digits only:', extractDigits(searchInput.value));
      }
    });
    
    // Handle input focus
    searchInput.addEventListener('focus', function() {
      dynamicPlaceholder.style.color = 'rgba(255, 255, 255, 0.3)';
    });
    
    searchInput.addEventListener('blur', function() {
      dynamicPlaceholder.style.color = 'rgba(255, 255, 255, 0.5)';
    });
    
    // Arrow click focuses on input
    searchArrow.addEventListener('click', function(e) {
      e.stopPropagation();
      searchInput.focus();
    });
    
    // Container click focuses on input
    document.getElementById('searchContainer').addEventListener('click', function() {
      searchInput.focus();
    });
  });
</script>

<div class="page-container">
  <div class="premier-logo-container">
    <img src="/premier-network-logo.png" alt="Premier Network" class="premier-logo">
  </div>
  <div class="custom-search-container" id="searchContainer">
    <div class="search-header">
      <svg class="keygen-logo" width="21" height="26" viewBox="0 0 21 26" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M21 6.27726L10.9152 16.7371L13.1269 18.821V18.8196L13.1282 18.821L10.3439 21.7096L7.09999 18.6552L15.9999 9.4206L16.0026 9.4233L18.1093 7.23563L16.1008 5.3445L15.8962 5.15174L10.4271 0L8.31901 2.18632L8.3381 2.20385L3.66385 7.05231L5.50601 8.78708L5.87553 9.13619L4.43153 10.6364H4.43017L4.63334 12.5276L2.798 12.3294L3.00526 14.2623L1.13038 14.0601L0 19.6109L10.0834 9.14967L8.25765 7.43108L7.87176 7.06579L7.8704 7.06714H7.86903L10.5498 4.28638L13.7882 7.33807L2.78164 18.7576L2.78709 18.7644L10.4707 26L12.5774 23.8137L12.5555 23.7935L17.3975 18.7698L15.1858 16.6859H15.1845L16.5671 15.2517L16.5685 15.2503L16.3653 13.3592L18.2006 13.5574L17.9934 11.6244L19.8683 11.8266L21 6.27726Z" fill="#F5F5F5"/>
      </svg>
      <span class="custom-search-text">Keygen Distribution Portal</span>
    </div>
    <div class="input-wrapper">
        <svg class="custom-search-arrow" id="searchArrow" width="21" height="12" viewBox="0 0 21 12" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M4.62699 0.0242505L3.65678 1.70777L3.65226 1.70778L3.65355 2.56856L2.96391 2.5696L0.00601632 4.08839L0.00736738 4.98627L0.00914554 6.16799L0.00932936 6.29015L0.0104966 7.06586L2.97295 8.57575L3.66259 8.57471L3.66387 9.42784L4.64368 11.1161L6.22458 11.1137L7.4289 9.42257L7.42891 9.42983L9.13861 9.42726L9.85905 8.56539L10.0718 8.56507L12.5147 8.56139L13.9501 7.29204L15.3025 8.5572L16.7375 7.28784L18.0907 8.553L20.4862 6.01501L11.0098 6.02927L11.0084 5.09188L20.4848 5.07762L18.0816 2.54685L16.7322 3.81608L15.2935 2.55105L13.9449 3.82027L12.5057 2.55524L10.0627 2.55892L9.85001 2.55924L9.12698 1.69954L7.41729 1.70211L7.41194 1.70212L6.20789 0.0218716L4.62699 0.0242505Z" fill="white"/>
            <path d="M4.58922 3.83231L6.48839 5.60021L6.86554 5.21138L7.39009 5.69924L6.8371 6.26977L5.16085 4.70957L5.16085 4.70917L4.76404 4.33964L4.4214 4.69294L4.38689 4.72888L3.45428 5.69065L3.85109 6.06017L3.85437 6.05694L4.73453 6.87609L5.04841 6.55227L5.11168 6.48726L5.38405 6.74045L5.72676 6.70445L5.69144 7.02665L6.04197 6.98983L6.00584 7.31929L7.01221 7.51613L5.11304 5.74863L4.80203 6.06923L4.80203 6.06963L4.73588 6.13746L4.7363 6.13786L4.23153 5.66811L4.7837 5.0984L6.85676 7.02812L6.85799 7.02691L8.16775 5.6759L7.77094 5.30638L7.76724 5.31042L6.85495 4.46148L6.47821 4.85031L6.4778 4.85072L6.21738 4.60799L5.87467 4.64439L5.90998 4.32179L5.55987 4.35861L5.596 4.02956L4.58922 3.83231Z" fill="#020910"/>
          </svg>
      <div id="dynamicPlaceholder" class="dynamic-placeholder">XXXXX-XXXXX-XXXXXX</div>
      <input type="text" class="custom-search-input" id="searchInput" placeholder="" data-placeholder="XXXXX-XXXXX-XXXXXX">
    </div>
  </div>
  <div class="footer-text">
    <p>How do i get a <svg class="footer-logo" width="21" height="26" viewBox="0 0 21 26" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M21 6.27726L10.9152 16.7371L13.1269 18.821V18.8196L13.1282 18.821L10.3439 21.7096L7.09999 18.6552L15.9999 9.4206L16.0026 9.4233L18.1093 7.23563L16.1008 5.3445L15.8962 5.15174L10.4271 0L8.31901 2.18632L8.3381 2.20385L3.66385 7.05231L5.50601 8.78708L5.87553 9.13619L4.43153 10.6364H4.43017L4.63334 12.5276L2.798 12.3294L3.00526 14.2623L1.13038 14.0601L0 19.6109L10.0834 9.14967L8.25765 7.43108L7.87176 7.06579L7.8704 7.06714H7.86903L10.5498 4.28638L13.7882 7.33807L2.78164 18.7576L2.78709 18.7644L10.4707 26L12.5774 23.8137L12.5555 23.7935L17.3975 18.7698L15.1858 16.6859H15.1845L16.5671 15.2517L16.5685 15.2503L16.3653 13.3592L18.2006 13.5574L17.9934 11.6244L19.8683 11.8266L21 6.27726Z" fill="currentColor"/>
    </svg> Entry Code</p>
    <p>What happens after i enter the <svg class="footer-logo" width="21" height="26" viewBox="0 0 21 26" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M21 6.27726L10.9152 16.7371L13.1269 18.821V18.8196L13.1282 18.821L10.3439 21.7096L7.09999 18.6552L15.9999 9.4206L16.0026 9.4233L18.1093 7.23563L16.1008 5.3445L15.8962 5.15174L10.4271 0L8.31901 2.18632L8.3381 2.20385L3.66385 7.05231L5.50601 8.78708L5.87553 9.13619L4.43153 10.6364H4.43017L4.63334 12.5276L2.798 12.3294L3.00526 14.2623L1.13038 14.0601L0 19.6109L10.0834 9.14967L8.25765 7.43108L7.87176 7.06579L7.8704 7.06714H7.86903L10.5498 4.28638L13.7882 7.33807L2.78164 18.7576L2.78709 18.7644L10.4707 26L12.5774 23.8137L12.5555 23.7935L17.3975 18.7698L15.1858 16.6859H15.1845L16.5671 15.2517L16.5685 15.2503L16.3653 13.3592L18.2006 13.5574L17.9934 11.6244L19.8683 11.8266L21 6.27726Z" fill="currentColor"/>
    </svg> Entry Code?</p>
  </div>
</div>

<style>
  /* New container for page centering */
  .page-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: 80px 20px; /* Add vertical padding to create space from header/footer */
    box-sizing: border-box;
  }
  
  .premier-logo-container {
    margin-bottom: 40px;
    text-align: center;
  }
  
  .premier-logo {
    max-width: 200px;
    height: auto;
  }
  
  .footer-text {
    margin-top: 24px;
    text-align: center;
  }
  
  .footer-text p {
    font-family: 'Inter', sans-serif;
    font-weight: 300;
    font-size: 12px;
    color: #000000;
    margin: 0;
    line-height: 1.5;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 4px;
  }

  .footer-logo {
    width: 12px;
    height: auto;
    color: #000000;
    display: inline-block;
    vertical-align: middle;
    margin: 0 2px;
  }
  .footer-text p:first-child {
    margin-bottom: 8px; /* Space between the two lines */
  }
  
  .custom-search-container {
    position: relative;
    display: flex;
    flex-direction: column;
    background: #000000;
    border-radius: 14px;
    padding: 16px 20px 20px;
    width: 400px;
    max-width: 400px;
    height: auto;
    min-height: 170px;
    cursor: pointer;
    box-sizing: border-box;
    margin: 0 auto;
    border: none;
    position: relative;
    z-index: 1;
  }
  
  /* Fix gradient border with proper thickness */
  .custom-search-container::before {
    content: "";
    position: absolute;
    top: -4px;
    left: -4px;
    right: -4px;
    bottom: -4px;
    z-index: -1;
    border-radius: 18px;
    background: linear-gradient(45deg, 
      #ff0000, #ff7300, #fffb00, #48ff00, 
      #00ffd5, #002bff, #7a00ff, #ff00c8, #ff0000);
    background-size: 400%;
    animation: borderGradient 10s linear infinite;
  }
  
  .custom-search-container::after {
    content: "";
    position: absolute;
    top: 2px;
    left: 2px;
    right: 2px;
    bottom: 2px;
    background: #111111;
    border-radius: 10px;
    z-index: -1;
  }
  
  @keyframes borderGradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  .search-header {
    display: flex;
    align-items: center;
    margin-bottom: 24px;
    margin-top: 4px;
  }
  
  .keygen-logo {
    margin-right: 12px;
    fill: #d71a22;
    height: 24px;
    width: auto;
  }
  
  .custom-search-text {
    color: #fff;
    font-family: poppins, sans-serif;
    font-size: 16px; /* Responsive font size */
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    text-shadow: 0 0 8px rgba(237, 28, 36, 0.5);
  }
  
  .input-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    width: 65%; /* Reduced from 100% */
    margin: 8px auto 0; 
    border-radius: 10px;
    z-index: 1;
  }
  
  /* Fix input gradient border */
  .input-wrapper::before {
    content: "";
    position: absolute;
    top: -1px;
    left: -1px;
    right: -1px;
    bottom: -1px;
    background: linear-gradient(45deg, 
      #ff0000, #ff7300, #fffb00, #48ff00, 
      #00ffd5, #002bff, #7a00ff, #ff00c8, #ff0000);
    background-size: 400%;
    border-radius: 12px;
    z-index: -1;
    animation: borderGradient 10s linear infinite;
  }
  
  .input-wrapper::after {
    content: "";
    position: absolute;
    top: 2px;
    left: 2px;
    right: 2px;
    bottom: 2px;
    background: rgba(20, 20, 20, 0.9);
    border-radius: 8px;
    z-index: -1;
  }
  
  /* Remove red hover effects */
  .custom-search-container:hover {
    box-shadow: none;
    border-color: transparent;
  }
  
  .custom-search-input:focus {
    border-color: transparent;
    box-shadow: none;
  }
  
  /* Update hover effect to enhance gradient only */
  .custom-search-container:hover::before,
  .input-wrapper:hover::before {
    animation: borderGradient 3s linear infinite;
    filter: brightness(1.2) saturate(1.5);
  }
  
  /* Fix z-index issues */
  .custom-search-input {
    background: transparent;
    border-radius: 10px;
    outline: none;
    color: #ffffff;
    font-family: monospace;
    font-size: clamp(14px, 4vw, 16px);
    width: 100%;
    padding: 12px 10px 12px 42px;
    letter-spacing: 1.5px;
    height: 46px;
    position: relative;
    z-index: 2;
    box-sizing: border-box;
    border: none;
  }
  
  .custom-search-arrow {
    position: absolute;
    left: 12px;
    width: 21px;
    height: 12px;
    cursor: pointer;
    fill: #d71a22;
    z-index: 3;
  }
  
  .dynamic-placeholder {
    position: absolute;
    left: 42px;
    top: 13px;
    color: rgba(255, 255, 255, 0.5);
    font-family: monospace;
    font-size: clamp(14px, 4vw, 16px);
    letter-spacing: 1.5px;
    pointer-events: none;
    z-index: 2;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: calc(100% - 52px);
  }
  </style>