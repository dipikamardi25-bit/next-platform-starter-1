<!doctype html>
<html lang="en" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flat Maintenance Lookup</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&amp;display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
      font-family: 'DM Sans', sans-serif;
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full">
  <div id="app-wrapper" class="h-full w-full overflow-auto" style="background: #0f172a;"><!-- Decorative gradient orbs -->
   <div style="position: fixed; top: -100px; right: -100px; width: 400px; height: 400px; background: radial-gradient(circle, rgba(99, 102, 241, 0.15) 0%, transparent 70%); pointer-events: none;"></div>
   <div style="position: fixed; bottom: -150px; left: -150px; width: 500px; height: 500px; background: radial-gradient(circle, rgba(16, 185, 129, 0.1) 0%, transparent 70%); pointer-events: none;"></div>
   <div class="min-h-full flex flex-col items-center justify-center p-6 relative"><!-- Main Card -->
    <div class="w-full max-w-md" style="background: linear-gradient(145deg, #1e293b 0%, #0f172a 100%); border: 1px solid rgba(99, 102, 241, 0.2); border-radius: 24px; box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(255,255,255,0.05) inset;"><!-- Header -->
     <div class="p-6 pb-4 border-b" style="border-color: rgba(99, 102, 241, 0.1);">
      <div class="flex items-center gap-3">
       <div class="w-12 h-12 rounded-xl flex items-center justify-center" style="background: linear-gradient(135deg, #6366f1 0%, #4f46e5 100%); box-shadow: 0 4px 15px rgba(99, 102, 241, 0.4);">
        <svg width="24" height="24" viewbox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path> <polyline points="9 22 9 12 15 12 15 22"></polyline>
        </svg>
       </div>
       <div>
        <h1 id="app-title" class="text-xl font-bold" style="color: #f1f5f9;">Flat Maintenance Lookup</h1>
        <p class="text-sm" style="color: #64748b;">Search resident balance info</p>
       </div>
      </div>
     </div><!-- Search Section -->
     <div class="p-6"><label id="search-label" for="flat-input" class="block text-sm font-medium mb-2" style="color: #94a3b8;">Enter Flat Number</label>
      <div class="relative"><input type="text" id="flat-input" placeholder="e.g., A-101, B-205" class="w-full px-4 py-3 rounded-xl text-base outline-none transition-all duration-200" style="background: rgba(30, 41, 59, 0.8); border: 2px solid rgba(99, 102, 241, 0.2); color: #f1f5f9;" onfocus="this.style.borderColor='rgba(99, 102, 241, 0.6)'; this.style.boxShadow='0 0 0 4px rgba(99, 102, 241, 0.1)'" onblur="this.style.borderColor='rgba(99, 102, 241, 0.2)'; this.style.boxShadow='none'"> <button id="search-btn" onclick="lookupFlat()" class="absolute right-2 top-1/2 -translate-y-1/2 px-4 py-2 rounded-lg font-medium text-sm transition-all duration-200" style="background: linear-gradient(135deg, #6366f1 0%, #4f46e5 100%); color: white;" onmouseover="this.style.transform='translateY(-50%) scale(1.05)'; this.style.boxShadow='0 4px 15px rgba(99, 102, 241, 0.4)'" onmouseout="this.style.transform='translateY(-50%) scale(1)'; this.style.boxShadow='none'"> Search </button>
      </div><!-- Quick Select Buttons -->
      <div class="mt-4 flex flex-wrap gap-2"><span class="text-xs" style="color: #64748b;">Quick select:</span> <button onclick="quickSelect('A-101')" class="px-3 py-1 rounded-full text-xs font-medium transition-all" style="background: rgba(99, 102, 241, 0.1); color: #818cf8; border: 1px solid rgba(99, 102, 241, 0.2);" onmouseover="this.style.background='rgba(99, 102, 241, 0.2)'" onmouseout="this.style.background='rgba(99, 102, 241, 0.1)'">A-101</button> <button onclick="quickSelect('A-102')" class="px-3 py-1 rounded-full text-xs font-medium transition-all" style="background: rgba(99, 102, 241, 0.1); color: #818cf8; border: 1px solid rgba(99, 102, 241, 0.2);" onmouseover="this.style.background='rgba(99, 102, 241, 0.2)'" onmouseout="this.style.background='rgba(99, 102, 241, 0.1)'">A-102</button> <button onclick="quickSelect('B-201')" class="px-3 py-1 rounded-full text-xs font-medium transition-all" style="background: rgba(99, 102, 241, 0.1); color: #818cf8; border: 1px solid rgba(99, 102, 241, 0.2);" onmouseover="this.style.background='rgba(99, 102, 241, 0.2)'" onmouseout="this.style.background='rgba(99, 102, 241, 0.1)'">B-201</button> <button onclick="quickSelect('B-202')" class="px-3 py-1 rounded-full text-xs font-medium transition-all" style="background: rgba(99, 102, 241, 0.1); color: #818cf8; border: 1px solid rgba(99, 102, 241, 0.2);" onmouseover="this.style.background='rgba(99, 102, 241, 0.2)'" onmouseout="this.style.background='rgba(99, 102, 241, 0.1)'">B-202</button>
      </div>
     </div><!-- Results Section -->
     <div id="results" class="px-6 pb-6 hidden">
      <div class="rounded-xl overflow-hidden" style="background: rgba(30, 41, 59, 0.5); border: 1px solid rgba(99, 102, 241, 0.1);"><!-- Result Header -->
       <div class="px-4 py-3 flex items-center gap-2" style="background: rgba(99, 102, 241, 0.1); border-bottom: 1px solid rgba(99, 102, 241, 0.1);">
        <svg width="16" height="16" viewbox="0 0 24 24" fill="none" stroke="#10b981" stroke-width="2"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"></path> <polyline points="22 4 12 14.01 9 11.01"></polyline>
        </svg><span class="text-sm font-medium" style="color: #10b981;">Record Found</span>
       </div><!-- Result Content -->
       <div class="p-4 space-y-4"><!-- Flat Number -->
        <div class="flex justify-between items-center"><span class="text-sm" style="color: #64748b;">Flat Number</span> <span id="result-flat" class="font-semibold" style="color: #f1f5f9;">-</span>
        </div><!-- Owner Name -->
        <div class="flex justify-between items-center"><span class="text-sm" style="color: #64748b;">Owner Name</span> <span id="result-name" class="font-semibold" style="color: #f1f5f9;">-</span>
        </div><!-- Contact -->
        <div class="flex justify-between items-center"><span class="text-sm" style="color: #64748b;">Contact</span> <span id="result-contact" class="font-semibold" style="color: #f1f5f9;">-</span>
        </div>
        <div class="h-px" style="background: rgba(99, 102, 241, 0.1);"></div><!-- Balance Display -->
        <div class="rounded-xl p-4 text-center" style="background: linear-gradient(135deg, rgba(16, 185, 129, 0.1) 0%, rgba(16, 185, 129, 0.05) 100%); border: 1px solid rgba(16, 185, 129, 0.2);"><span class="text-sm block mb-1" style="color: #64748b;">Maintenance Balance</span> <span id="result-balance" class="text-3xl font-bold" style="color: #10b981;">₹0</span>
        </div><!-- Last Payment -->
        <div class="flex justify-between items-center text-sm"><span style="color: #64748b;">Last Payment</span> <span id="result-lastpaid" style="color: #94a3b8;">-</span>
        </div>
       </div>
      </div>
     </div><!-- Error Section -->
     <div id="error" class="px-6 pb-6 hidden">
      <div class="rounded-xl p-4 text-center" style="background: rgba(239, 68, 68, 0.1); border: 1px solid rgba(239, 68, 68, 0.2);">
       <svg class="mx-auto mb-2" width="32" height="32" viewbox="0 0 24 24" fill="none" stroke="#ef4444" stroke-width="2"><circle cx="12" cy="12" r="10"></circle> <line x1="12" y1="8" x2="12" y2="12"></line> <line x1="12" y1="16" x2="12.01" y2="16"></line>
       </svg>
       <p id="error-message" class="font-medium" style="color: #ef4444;">Flat not found</p>
       <p class="text-sm mt-1" style="color: #64748b;">Please check the flat number and try again</p>
      </div>
     </div><!-- Footer -->
     <div class="px-6 pb-6">
      <p class="text-center text-xs" style="color: #475569;">Formula: =VLOOKUP(FlatNo, Data!A:E, Column, FALSE)</p>
     </div>
    </div>
   </div>
  </div>
  <script>
    // Sample data simulating Excel sheet (Data!A:E)
    // Column A: Flat No, B: Name, C: Contact, D: Balance, E: Last Paid
    const data = [
      { flatNo: 'A-101', name: 'Rajesh Sharma', contact: '9876543210', balance: 15000, lastPaid: '15 Nov 2024' },
      { flatNo: 'A-102', name: 'Priya Patel', contact: '9876543211', balance: 0, lastPaid: '01 Dec 2024' },
      { flatNo: 'A-103', name: 'Amit Kumar', contact: '9876543212', balance: 7500, lastPaid: '20 Oct 2024' },
      { flatNo: 'B-201', name: 'Sneha Gupta', contact: '9876543213', balance: 22500, lastPaid: '05 Sep 2024' },
      { flatNo: 'B-202', name: 'Vikram Singh', contact: '9876543214', balance: 3000, lastPaid: '28 Nov 2024' },
      { flatNo: 'B-203', name: 'Ananya Reddy', contact: '9876543215', balance: 0, lastPaid: '01 Dec 2024' },
      { flatNo: 'C-301', name: 'Karan Mehta', contact: '9876543216', balance: 45000, lastPaid: '10 Jul 2024' },
      { flatNo: 'C-302', name: 'Divya Nair', contact: '9876543217', balance: 11250, lastPaid: '22 Oct 2024' },
    ];

    // VLOOKUP function simulation
    function vlookup(searchValue, dataArray, columnIndex) {
      const normalizedSearch = searchValue.toUpperCase().trim();
      const record = dataArray.find(row => row.flatNo.toUpperCase() === normalizedSearch);
      
      if (!record) return null;
      
      const columns = ['flatNo', 'name', 'contact', 'balance', 'lastPaid'];
      return record[columns[columnIndex - 1]];
    }

    function lookupFlat() {
      const input = document.getElementById('flat-input').value;
      const resultsDiv = document.getElementById('results');
      const errorDiv = document.getElementById('error');
      
      if (!input.trim()) {
        resultsDiv.classList.add('hidden');
        errorDiv.classList.remove('hidden');
        document.getElementById('error-message').textContent = 'Please enter a flat number';
        return;
      }

      // Using VLOOKUP-style lookups
      const flatNo = vlookup(input, data, 1);
      const ownerName = vlookup(input, data, 2);
      const contact = vlookup(input, data, 3);
      const balance = vlookup(input, data, 4);
      const lastPaid = vlookup(input, data, 5);

      if (ownerName === null) {
        resultsDiv.classList.add('hidden');
        errorDiv.classList.remove('hidden');
        document.getElementById('error-message').textContent = `Flat "${input}" not found`;
        return;
      }

      // Display results
      errorDiv.classList.add('hidden');
      resultsDiv.classList.remove('hidden');
      
      document.getElementById('result-flat').textContent = flatNo;
      document.getElementById('result-name').textContent = ownerName;
      document.getElementById('result-contact').textContent = contact;
      document.getElementById('result-balance').textContent = '₹' + balance.toLocaleString('en-IN');
      document.getElementById('result-lastpaid').textContent = lastPaid;

      // Update balance color based on amount
      const balanceEl = document.getElementById('result-balance');
      const balanceContainer = balanceEl.parentElement;
      
      if (balance === 0) {
        balanceEl.style.color = '#10b981';
        balanceContainer.style.background = 'linear-gradient(135deg, rgba(16, 185, 129, 0.1) 0%, rgba(16, 185, 129, 0.05) 100%)';
        balanceContainer.style.borderColor = 'rgba(16, 185, 129, 0.2)';
      } else if (balance > 20000) {
        balanceEl.style.color = '#ef4444';
        balanceContainer.style.background = 'linear-gradient(135deg, rgba(239, 68, 68, 0.1) 0%, rgba(239, 68, 68, 0.05) 100%)';
        balanceContainer.style.borderColor = 'rgba(239, 68, 68, 0.2)';
      } else {
        balanceEl.style.color = '#f59e0b';
        balanceContainer.style.background = 'linear-gradient(135deg, rgba(245, 158, 11, 0.1) 0%, rgba(245, 158, 11, 0.05) 100%)';
        balanceContainer.style.borderColor = 'rgba(245, 158, 11, 0.2)';
      }

      // Add animation
      resultsDiv.style.animation = 'none';
      resultsDiv.offsetHeight;
      resultsDiv.style.animation = 'slideIn 0.3s ease-out';
    }

    function quickSelect(flatNo) {
      document.getElementById('flat-input').value = flatNo;
      lookupFlat();
    }

    // Enter key support
    document.getElementById('flat-input').addEventListener('keypress', function(e) {
      if (e.key === 'Enter') {
        lookupFlat();
      }
    });

    // Default config
    const defaultConfig = {
      app_title: 'Flat Maintenance Lookup',
      search_label: 'Enter Flat Number',
      background_color: '#0f172a',
      card_color: '#1e293b',
      text_color: '#f1f5f9',
      accent_color: '#6366f1',
      success_color: '#10b981'
    };

    let config = { ...defaultConfig };

    async function onConfigChange(newConfig) {
      config = { ...defaultConfig, ...newConfig };
      
      const customFont = config.font_family || 'DM Sans';
      const baseFontStack = 'sans-serif';
      const fontStack = `${customFont}, ${baseFontStack}`;
      
      document.body.style.fontFamily = fontStack;
      
      // Update text content
      document.getElementById('app-title').textContent = config.app_title || defaultConfig.app_title;
      document.getElementById('search-label').textContent = config.search_label || defaultConfig.search_label;
      
      // Update colors
      document.getElementById('app-wrapper').style.background = config.background_color || defaultConfig.background_color;
      
      // Update accent colors
      const accentColor = config.accent_color || defaultConfig.accent_color;
      document.getElementById('search-btn').style.background = `linear-gradient(135deg, ${accentColor} 0%, ${adjustColor(accentColor, -20)} 100%)`;
    }

    function adjustColor(hex, percent) {
      const num = parseInt(hex.replace('#', ''), 16);
      const amt = Math.round(2.55 * percent);
      const R = Math.max(0, Math.min(255, (num >> 16) + amt));
      const G = Math.max(0, Math.min(255, (num >> 8 & 0x00FF) + amt));
      const B = Math.max(0, Math.min(255, (num & 0x0000FF) + amt));
      return '#' + (0x1000000 + R * 0x10000 + G * 0x100 + B).toString(16).slice(1);
    }

    function mapToCapabilities(config) {
      return {
        recolorables: [
          {
            get: () => config.background_color || defaultConfig.background_color,
            set: (value) => { config.background_color = value; window.elementSdk.setConfig({ background_color: value }); }
          },
          {
            get: () => config.card_color || defaultConfig.card_color,
            set: (value) => { config.card_color = value; window.elementSdk.setConfig({ card_color: value }); }
          },
          {
            get: () => config.text_color || defaultConfig.text_color,
            set: (value) => { config.text_color = value; window.elementSdk.setConfig({ text_color: value }); }
          },
          {
            get: () => config.accent_color || defaultConfig.accent_color,
            set: (value) => { config.accent_color = value; window.elementSdk.setConfig({ accent_color: value }); }
          },
          {
            get: () => config.success_color || defaultConfig.success_color,
            set: (value) => { config.success_color = value; window.elementSdk.setConfig({ success_color: value }); }
          }
        ],
        borderables: [],
        fontEditable: {
          get: () => config.font_family || 'DM Sans',
          set: (value) => { config.font_family = value; window.elementSdk.setConfig({ font_family: value }); }
        },
        fontSizeable: undefined
      };
    }

    function mapToEditPanelValues(config) {
      return new Map([
        ['app_title', config.app_title || defaultConfig.app_title],
        ['search_label', config.search_label || defaultConfig.search_label]
      ]);
    }

    // Initialize SDK
    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig,
        onConfigChange,
        mapToCapabilities,
        mapToEditPanelValues
      });
    }

    // Add animation styles
    const style = document.createElement('style');
    style.textContent = `
      @keyframes slideIn {
        from {
          opacity: 0;
          transform: translateY(-10px);
        }
        to {
          opacity: 1;
          transform: translateY(0);
        }
      }
    `;
    document.head.appendChild(style);
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9c046844f772755c',t:'MTc2ODgwNTUyNi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html> 

Create
