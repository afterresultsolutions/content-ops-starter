<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>AfterResult Quotation Estimator</title>
<style>
  body {
    font-family: "Inter", Arial, sans-serif;
    background: #000;
    color: #ddd;
    margin: 0;
    padding: 20px;
  }
  #calculatorContainer {
    max-width: 900px;
    width: 100%;
    margin: 20px auto;
    padding: 15px;
    background: #181818;
    border-radius: 18px;
    border: 2px solid #f39c12;
    box-shadow: 0 0 40px #f39c12;
    box-sizing: border-box;
  }
  h2, h3 {
    color: #f39c12;
    font-weight: 400;
    font-size: 1.5rem;
    text-align: center;
    margin-bottom: 15px;
  }
  label {
    display: block;
    font-size: 13px;
    color: #ccc;
    margin-bottom: 5px;
    font-weight: 300;
  }
  select,
  input[type="number"],
  input[type="text"],
  input[type="email"],
  input[type="tel"] {
    width: 100%;
    padding: 8px 14px;
    border-radius: 20px;
    border: 2px solid #f39c12;
    background: #111;
    color: #fff;
    font-size: 14px;
    margin-bottom: 14px;
    outline: none;
    transition: border-color 0.3s;
    text-align: left;
  }
  select:hover,
  select:focus,
  input:hover,
  input:focus {
    border-color: #e67e22;
  }
  .button-row {
    display: flex;
    gap: 12px;
    margin-bottom: 12px;
    margin-top: 8px;
    flex-wrap: wrap;
  }
  button {
    flex: 1;
    padding: 10px 0;
    border: none;
    border-radius: 25px;
    background: linear-gradient(90deg, #f39c12 0%, #e74c3c 100%);
    color: white;
    font-weight: 600;
    font-size: 0.80rem;
    cursor: pointer;
    margin-bottom: 0;
    transition: background 0.3s;
    min-width: 120px;
  }
  button.whatsapp {
    background: linear-gradient(90deg, #25d366 0%, #128c7e 100%);
  }
  button:hover {
    background: linear-gradient(90deg, #e67e22 0%, #c0392b 100%);
  }
  button.whatsapp:hover {
    background: linear-gradient(90deg, #128c7e 0%, #25d366 100%);
  }
  .hidden {
    display: none !important;
  }
  #estimatedPriceRange {
    color: #f39c12;
    font-weight: 600;
    font-size: 0.8rem;
    min-height: 24px;
    margin-bottom: 8px;
    white-space: pre-line;
    text-align: center;
  }
  #averagePriceRange {
    color: #aaa;
    font-weight: 400;
    font-size: 0.7rem;
    margin-bottom: 16px;
    text-align: center;
    font-style: italic;
  }
  .slider-row {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 14px;
    justify-content: center;
  }
  .slider-row label {
    margin: 0 0 0 0;
    font-size: 0.9em;
    color: #bbb;
    font-weight: 400;
  }
  input[type="range"] {
    width: 240px;
    accent-color: #f39c12;
    height: 3px;
    background: linear-gradient(90deg, #f39c12 0%, #e74c3c 100%);
    border-radius: 2px;
    outline: none;
    margin: 0;
    -webkit-appearance: none;
  }
  input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 10px;
    height: 18px;
    border-radius: 50%;
    background: #fff;
    border: 2px solid #f39c12;
    box-shadow: 0 2px 8px #0002;
    cursor: pointer;
    transition: background 0.2s;
  }
  input[type="range"]:focus::-webkit-slider-thumb {
    background: #f39c12;
    border-color: #e67e22;
  }
  input[type="range"]::-moz-range-thumb {
    width: 10px;
    height: 18px;
    border-radius: 50%;
    background: #fff;
    border: 2px solid #f39c12;
    box-shadow: 0 2px 8px #0002;
    cursor: pointer;
    transition: background 0.2s;
  }
  input[type="range"]:focus::-moz-range-thumb {
    background: #f39c12;
    border-color: #e67e22;
  }
  input[type="range"]::-ms-thumb {
    width: 10px;
    height: 18px;
    border-radius: 50%;
    background: #fff;
    border: 2px solid #f39c12;
    box-shadow: 0 2px 8px #0002;
    cursor: pointer;
    transition: background 0.2s;
  }
  .centered-checkboxes {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
    font-size: 0.85em;
    margin-bottom: 6px;
  }
  #quotePreviewSection {
    background: #fff;
    color: #222;
    border-radius: 10px;
    padding: 15px;
    box-shadow: 0 0 20px #f39c12;
    margin-top: 25px;
    font-family: "Inter", Arial, sans-serif;
    font-size: 13px;
    max-width: 500px;
    position: relative;
    overflow-x: auto;
  }
  #quotePreviewContent {
    max-width: 100%;
    margin: auto;
    text-align: left;
    word-wrap: break-word;
    position: relative;
    z-index: 2;
  }
  .watermark {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(-30deg);
    font-size: 5vw;
    color: rgba(243, 156, 18, 0.09);
    user-select: none;
    pointer-events: none;
    font-weight: 900;
    letter-spacing: 10px;
    white-space: nowrap;
    z-index: 1;
  }
  .quotation-header {
    display: flex;
    align-items: center;
    gap: 14px;
    border-bottom: 2px solid #f39c12;
    padding-bottom: 6px;
    margin-bottom: 15px;
    flex-wrap: wrap;
  }
  .quotation-header img {
    height: 50px;
    width: auto;
    border-radius: 8px;
    background: #fff;
    padding: 4px;
    flex-shrink: 0;
  }
  .quotation-meta {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-bottom: 8px;
    font-size: 11px;
  }
  .quotation-section-title {
    color: #f39c12;
    font-size: 14px;
    margin-top: 15px;
    margin-bottom: 6px;
    font-weight: 600;
  }
  .quotation-table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 12px;
    font-size: 13px;
  }
  .quotation-table th,
  .quotation-table td {
    border: 1px solid #ccc;
    padding: 6px 10px;
    text-align: left;
    font-size: 13px;
    font-weight: 400;
  }
  .quotation-table th {
    background: #f39c12;
    color: #fff;
    font-weight: 600;
    text-align: center;
  }
  .quotation-table td {
    text-align: center;
  }
  .quotation-table td.left {
    text-align: left;
  }
  .quotation-terms {
    font-size: 11px;
    color: #444;
    background: #f7f7f7;
    padding: 10px;
    border-radius: 6px;
    max-height: 120px;
    overflow-y: auto;
  }
  .quotation-sign {
    margin-top: 16px;
    font-size: 12px;
  }
  .qr-section {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-top: 16px;
    margin-bottom: 12px;
    flex-wrap: wrap;
  }
  .qr-section img {
    width: 70px;
    height: 70px;
    border-radius: 8px;
    border: 1px solid #ccc;
    background: #fff;
    padding: 2px;
  }
  .qr-section .website-link {
    font-size: 13px;
    color: #1d6fa5;
    font-weight: 600;
    text-decoration: underline;
    word-break: break-word;
  }
  /* Popup form styles */
  #popupFormOverlay {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0,0,0,0.85);
    display: none;
    justify-content: center;
    align-items: center;
    z-index: 9999;
  }
  #popupFormOverlay.show {
    display: flex;
  }
  #popupForm {
    background: #222;
    padding: 20px 25px;
    border-radius: 15px;
    max-width: 400px;
    width: 90%;
    box-sizing: border-box;
    box-shadow: 0 0 15px #f39c12;
  }
  #popupForm h3 {
    color: #f39c12;
    margin-top: 0;
    margin-bottom: 15px;
    font-weight: 400;
    text-align: center;
  }
  #popupForm label {
    color: #ccc;
    font-size: 13px;
    margin-bottom: 4px;
    display: block;
  }
  #popupForm input {
    width: 100%;
    padding: 8px 14px;
    border-radius: 20px;
    border: 2px solid #f39c12;
    background: #111;
    color: #fff;
    font-size: 14px;
    margin-bottom: 14px;
    outline: none;
    transition: border-color 0.3s;
    text-align: left;
  }
  #popupForm input:focus {
    border-color: #e67e22;
  }
  #popupForm .button-row {
    display: flex;
    justify-content: space-between;
    gap: 10px;
  }
  #popupForm button {
    flex: 1;
    padding: 10px 0;
    border: none;
    border-radius: 25px;
    background: linear-gradient(90deg, #f39c12 0%, #e74c3c 100%);
    color: white;
    font-weight: 700;
    font-size: 0.9rem;
    cursor: pointer;
    transition: background 0.3s;
  }
  #popupForm button:hover {
    background: linear-gradient(90deg, #e67e22 0%, #c0392b 100%);
  }
  /* Add New Service button */
  .add-service-btn {
    background: transparent !important;
    color: #888 !important;
    border: none !important;
    font-size: 12px !important;
    margin: -10px 0 12px 0 !important;
    padding: 5px 0 !important;
    width: auto !important;
    box-shadow: none !important;
    text-align: left;
    display: block;
    font-weight: 400;
    letter-spacing: 0.2px;
    cursor: pointer;
    transition: color 0.2s;
  }
  .add-service-btn:hover {
    color: #f39c12 !important;
    text-decoration: underline;
  }
  .remove-service-btn {
    background: transparent !important;
    color: #e74c3c !important;
    border: none !important;
    font-size: 18px !important;
    padding: 0 2px !important;
    margin-left: 5px !important;
    cursor: pointer;
    vertical-align: middle;
    line-height: 1;
    display: inline-block;
    transition: color 0.2s;
  }
  .remove-service-btn:hover {
    color: #c0392b !important;
  }
  .small-note, .small-btn, .small-label {
    font-size: 11px !important;
    color: #aaa !important;
  }
  .small-btn {
    padding: 3px 8px !important;
    border-radius: 16px !important;
    min-width: 70px !important;
    margin: 4px 0 0 0 !important;
    font-size: 12px !important;
  }
  .call-now-card {
    background: #fff;
    color: #c0392b;
    border-radius: 10px;
    padding: 12px 14px 10px 14px;
    box-shadow: 0 0 10px #e74c3c33;
    margin-top: 18px;
    font-size: 13px;
    position: relative;
    max-width: 400px;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
  }
  .call-now-card .close-call-card {
    position: absolute;
    top: 7px;
    right: 12px;
    color: #e74c3c;
    font-size: 18px;
    background: transparent;
    border: none;
    cursor: pointer;
    z-index: 2;
    padding: 0;
    line-height: 1;
  }
  .call-now-card .call-btn {
    background: transparent;
    color: #c0392b;
    border: 1px solid #e74c3c;
    border-radius: 16px;
    padding: 4px 16px;
    font-size: 13px;
    margin-top: 8px;
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
    font-weight: 600;
    transition: background 0.2s, color 0.2s;
  }
  .call-now-card .call-btn:hover {
    background: #e74c3c;
    color: #fff;
  }
  .other-platform-popup {
    background: #fff;
    color: #222;
    border-radius: 10px;
    padding: 16px;
    box-shadow: 0 0 10px #e74c3c33;
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
    z-index: 99999;
    min-width: 260px;
    max-width: 90vw;
    text-align: center;
  }
  .other-platform-popup input {
    width: 90%;
    margin-bottom: 10px;
    font-size: 14px;
  }
  .other-platform-popup .close-other-popup {
    position: absolute;
    top: 7px;
    right: 12px;
    color: #e74c3c;
    font-size: 18px;
    background: transparent;
    border: none;
    cursor: pointer;
    z-index: 2;
    padding: 0;
    line-height: 1;
  }
  /* Responsive */
  @media (max-width: 600px) {
    #calculatorContainer {
      padding: 3vw 1vw;
      font-size: 13px;
    }
    .quotation-table th, .quotation-table td {
      font-size: 12px;
      padding: 4px 6px;
    }
    .quotation-header img {
      height: 36px;
    }
    #quotePreviewSection {
      font-size: 12px;
      padding: 10px;
    }
    .call-now-card, .other-platform-popup {
      font-size: 12px;
      padding: 10px;
    }
    .slider-row label, label, .small-label {
      font-size: 11px !important;
    }
  }
</style>


<div id="calculatorContainer" role="main" aria-label="Quotation Estimator">
  <h2>AfterResult Quotation Estimator</h2>
  <div id="multiServiceList"></div>
  <div id="serviceFormSection"></div>
  <div id="estimatedPriceRange" aria-live="polite"></div>
  <div id="averagePriceRange" aria-live="polite"></div>
  <div class="button-row" id="mainBtnRow">
    <button id="previewQuotationBtn" type="button">Preview Quotation</button>
    <button id="whatsappQuotationBtn" type="button" class="whatsapp">Request Quotation via WhatsApp</button>
  </div>
  <div id="quotePreviewSection" class="hidden" aria-live="polite" aria-label="Quotation Preview">
    <div class="watermark">AfterResult</div>
    <div id="quotePreviewContent"></div>
    <button id="downloadQuoteBtn" type="button" style="margin-top: 10px; background: #222; color: #f39c12; border: none; padding: 8px 14px; border-radius: 20px; font-size: 12px; cursor: pointer; width: 100%;">Download Quotation as PDF</button>
    <button id="closePreviewBtn" type="button" style="margin-top: 10px; background: #222; color: #f39c12; border: none; padding: 8px 14px; border-radius: 20px; font-size: 12px; cursor: pointer; width: 100%;">Cancel / Back</button>
  </div>
  <div id="callNowCardContainer"></div>
</div>
<div id="popupFormOverlay" role="dialog" aria-modal="true" aria-labelledby="popupFormTitle" style="position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.85); display: none; justify-content: center; align-items: center; z-index: 9999;">
  <form id="popupForm" novalidate="" style="background: #222; padding: 20px 25px; border-radius: 15px; max-width: 400px; width: 90%; box-sizing: border-box; box-shadow: 0 0 15px #f39c12;">
    <h3 id="popupFormTitle" style="color:#f39c12; margin-top:0; margin-bottom:15px; font-weight:400; text-align:center;">Please Enter Your Details</h3>
    <label for="userName">Name *</label>
    <input type="text" id="userName" name="userName" required="" autocomplete="name">
    <label for="userPhone">Phone Number *</label>
    <input type="tel" id="userPhone" name="userPhone" pattern="^\+?\d{7,15}$" placeholder="+919999999999" required="" autocomplete="tel">
    <label for="userEmail">Email *</label>
    <input type="email" id="userEmail" name="userEmail" required="" autocomplete="email">
    <label for="userCompany">Company Name</label>
    <input type="text" id="userCompany" name="userCompany" autocomplete="organization">
    <div class="button-row" style="margin-top: 10px;">
      <button type="submit" id="popupSubmitBtn">Submit</button>
      <button type="button" id="popupCancelBtn" style="background:#555;">Cancel</button>
    </div>
  </form>
</div>

<div id="otherPlatformPopup" class="other-platform-popup hidden">
  <button class="close-other-popup" type="button" aria-label="Close">×</button>
  <div id="otherPlatformPopupContent"></div>
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrious/4.0.2/qrious.min.js"></script>
<script>
(() => {
  // --- DATA & CONFIG ---
  const COMPANY = {
    name: "AfterResult",
    address: "1438, Sector 2, 25th D Cross, HSR Layout, BDA Layout, HSR Layout, Bengaluru 560102",
    email: "contact@afterresult.com",
    phone: "+91 9599169901",
    logo: "https://www.afterresult.com/web/image/website/1/logo/AfterResult?unique=db83986",
    executive: "Suraj Pratap Singh",
    designation: "Business Development Executive",
    website: "https://afterresult.com",
    qr: "https://afterresult.com/web/image/website/1/logo/AfterResult?unique=db83986"
  };

  // Service definitions
  const SERVICE_CATEGORIES = [
    "Lifestyle", "Education", "Furniture", "Home Decor", "E-commerce", "Service-Based Business", "Other"
  ];

  const PROJECT_COMPLEXITY_LEVELS = [
    { val: "Basic", label: "Basic" },
    { val: "Moderate", label: "Moderate" },
    { val: "Advanced", label: "Advanced" }
  ];

  const SERVICE_DESCRIPTIONS = {
    "Logo Design": "Custom logo design tailored to your industry and brand identity.",
    "Basic Website": "A simple, responsive website suitable for small businesses or portfolios.",
    "Advanced Website": "A feature-rich, dynamic website for complex requirements.",
    "Social Media Management": "Management of your brand's social media presence across selected platforms.",
    "SEO Services": "Search Engine Optimization to improve your website's visibility and ranking.",
    "App Development": "Custom mobile application development for Android/iOS.",
    "Content Writing": "Professional content creation for websites, blogs, and social media.",
    "eCommerce Store": "Setup and customization of your online store on leading platforms.",
    "Marketplace Management": "End-to-end management of your products on online marketplaces.",
    "Digital Marketing": "Comprehensive digital marketing strategies for your business.",
    "Branding Services": "Brand strategy, identity, and collateral design services.",
    "Instagram Followers": "Boost your Instagram presence with real followers.",
    "Meta and Google Ads": "Setup and management of Meta (Facebook/Instagram) and Google Ad campaigns.",
    "3D or Product Design": "3D modeling and product design for your business needs.",
    "Other": "Custom service as per your requirements."
  };

  // Service pricing and options
  const SERVICES = [
    {
      key: "Logo Design",
      label: "Logo Design",
      price: 4000,
      min: 4000,
      max: 4000,
      avg: 4000,
      desc: SERVICE_DESCRIPTIONS["Logo Design"],
      options: {
        industry: true,
        complexity: true,
        category: true
      }
    },
    {
      key: "Basic Website",
      label: "Basic Website",
      min: 15000,
      max: 25000,
      avg: 20000,
      desc: SERVICE_DESCRIPTIONS["Basic Website"],
      options: {
        duration: true,
        complexity: true,
        category: true
      }
    },
    {
      key: "Advanced Website",
      label: "Advanced Website",
      min: 30000,
      max: 65000,
      avg: 47500,
      desc: SERVICE_DESCRIPTIONS["Advanced Website"],
      options: {
        duration: true,
        complexity: true,
        category: true
      }
    },
    {
      key: "Social Media Management",
      label: "Social Media Management",
      min: 7999,
      max: 11999,
      avg: 9999,
      desc: SERVICE_DESCRIPTIONS["Social Media Management"],
      options: {
        platforms: true,
        duration: true,
        category: true
      }
    },
    {
      key: "SEO Services",
      label: "SEO Services",
      min: 5000,
      max: 14000,
      avg: 9500,
      desc: SERVICE_DESCRIPTIONS["SEO Services"],
      options: {
        seoType: true,
        category: true
      }
    },
    {
      key: "App Development",
      label: "App Development",
      min: 35000,
      max: 120000,
      avg: 77500,
      desc: SERVICE_DESCRIPTIONS["App Development"],
      options: {
        duration: true,
        complexity: true,
        category: true
      }
    },
    {
      key: "Content Writing",
      label: "Content Writing",
      min: 2000,
      max: 12000,
      avg: 7000,
      desc: SERVICE_DESCRIPTIONS["Content Writing"],
      options: {
        category: true
      }
    },
    {
      key: "eCommerce Store",
      label: "eCommerce Store",
      min: 33250,
      max: 49800,
      avg: 41500,
      desc: SERVICE_DESCRIPTIONS["eCommerce Store"],
      options: {
        ecommerceType: true,
        complexity: true,
        category: true
      }
    },
    {
      key: "Marketplace Management",
      label: "Marketplace Management",
      min: 8000,
      max: 18000,
      avg: 13000,
      desc: SERVICE_DESCRIPTIONS["Marketplace Management"],
      options: {
        productCount: true,
        marketplacePlatforms: true,
        category: true
      }
    },
    {
      key: "Digital Marketing",
      label: "Digital Marketing",
      min: 12000,
      max: 30000,
      avg: 21000,
      desc: SERVICE_DESCRIPTIONS["Digital Marketing"],
      options: {
        duration: true,
        complexity: true,
        category: true
      }
    },
    {
      key: "Branding Services",
      label: "Branding Services",
      min: 10000,
      max: 30000,
      avg: 20000,
      desc: SERVICE_DESCRIPTIONS["Branding Services"],
      options: {
        brandingMedium: true,
        category: true
      }
    },
    {
      key: "Instagram Followers",
      label: "Instagram Followers",
      min: 500,
      max: 5000,
      avg: 2750,
      desc: SERVICE_DESCRIPTIONS["Instagram Followers"],
      options: {
        followers: true
      }
    },
    {
      key: "Meta and Google Ads",
      label: "Meta Ads and Google Ads",
      min: 2000,
      max: 35000,
      avg: 17500,
      desc: SERVICE_DESCRIPTIONS["Meta and Google Ads"],
      options: {
        adsType: true,
        campaignObjective: true,
        marketingBudget: true
      }
    },
    {
      key: "3D or Product Design",
      label: "3D or Product Design",
      min: 6000,
      max: 60000,
      avg: 33000,
      desc: SERVICE_DESCRIPTIONS["3D or Product Design"],
      options: {
        productName: true,
        productCategory: true,
        productCount: true,
        category: true
      }
    },
    {
      key: "Other",
      label: "Other (Request Quote)",
      min: 0,
      max: 0,
      avg: 0,
      desc: SERVICE_DESCRIPTIONS["Other"],
      options: {}
    }
  ];

  // --- STATE ---
  let multiServiceArr = [
    // Each: { id, serviceKey, fields }
  ];
  let serviceCounter = 1;
  let currentServiceId = null; // id of the service being edited
  let userDetails = null;
  let lastPreviewedServiceIds = [];
  let otherPlatformPopupState = null; // {type, callback}
  let callNowCardVisible = false;

  // --- INIT ---
  // Load user details from localStorage
  if (window.localStorage) {
    try {
      userDetails = JSON.parse(localStorage.getItem("ar_user_details") || "null");
    } catch (e) { userDetails = null; }
  }

  // --- DOM ---
  const $serviceFormSection = document.getElementById("serviceFormSection");
  const $multiServiceList = document.getElementById("multiServiceList");
  const $estimatedPriceRange = document.getElementById("estimatedPriceRange");
  const $averagePriceRange = document.getElementById("averagePriceRange");
  const $previewQuotationBtn = document.getElementById("previewQuotationBtn");
  const $whatsappQuotationBtn = document.getElementById("whatsappQuotationBtn");
  const $quotePreviewSection = document.getElementById("quotePreviewSection");
  const $quotePreviewContent = document.getElementById("quotePreviewContent");
  const $downloadQuoteBtn = document.getElementById("downloadQuoteBtn");
  const $closePreviewBtn = document.getElementById("closePreviewBtn");
  const $popupFormOverlay = document.getElementById("popupFormOverlay");
  const $popupForm = document.getElementById("popupForm");
  const $popupCancelBtn = document.getElementById("popupCancelBtn");
  const $callNowCardContainer = document.getElementById("callNowCardContainer");
  const $otherPlatformPopup = document.getElementById("otherPlatformPopup");
  const $otherPlatformPopupContent = document.getElementById("otherPlatformPopupContent");

  function getServiceByKey(key) {
    return SERVICES.find(s => s.key === key || s.label === key);
  }

  // --- RENDERING ---

  function renderMultiServiceList() {
    let html = '';
    if (multiServiceArr.length > 0) {
      html += '<div style="margin-bottom:8px;">';
      multiServiceArr.forEach((svc, idx) => {
        const service = getServiceByKey(svc.serviceKey);
        html += `<span class="small-label" style="display:inline-block; margin-right:8px; margin-bottom:3px; background:#222; border-radius:12px; padding:3px 9px; border:1px solid #f39c12; color:#f39c12; font-weight:500; cursor:pointer;" data-id="${svc.id}" onclick="window.arEditService('${svc.id}')">${service.label || svc.serviceKey}</span>`;
        html += `<button class="remove-service-btn" title="Remove" aria-label="Remove service" onclick="window.arRemoveService('${svc.id}')" type="button" tabindex="0">&times;</button>`;
      });
      html += '</div>';
    }
    $multiServiceList.innerHTML = html;
  }

  function renderServiceForm(serviceId = null) {
    // If serviceId is null, add new; else edit existing
    let svcObj = null;
    if (serviceId) {
      svcObj = multiServiceArr.find(s => s.id === serviceId);
      currentServiceId = serviceId;
    } else {
      svcObj = { id: "svc" + serviceCounter++, serviceKey: "", fields: {} };
      currentServiceId = svcObj.id;
    }

    let selectedKey = svcObj.serviceKey;
    let html = '';
    // Service selector
    html += `<label for="serviceSelectMain" class="small-label">Select a Service</label>`;
    html += `<select id="serviceSelectMain" aria-label="Select a service" style="margin-bottom:8px;">`;
    html += `<option value="" disabled ${!selectedKey ? "selected" : ""}>-- Choose a service --</option>`;
    SERVICES.forEach(svc => {
      html += `<option value="${svc.key}" ${svc.key === selectedKey ? "selected" : ""}>${svc.label}</option>`;
    });
    html += `</select>`;
    html += `<button class="add-service-btn" id="addServiceBtn" type="button" tabindex="0">+ Add Another Service</button>`;

    // If service selected, show options
    if (selectedKey) {
      const service = getServiceByKey(selectedKey);
      // Description
      html += `<div class="small-note" style="margin-bottom:7px; color:#f39c12;">${service.desc || ""}</div>`;
      // Industry field (for logo, etc)
      if (service.options.industry) {
        html += `<label for="industryField" class="small-label">Industry</label>`;
        html += `<input type="text" id="industryField" value="${svcObj.fields.industry || ""}" maxlength="40" placeholder="e.g. Education, Tech, etc.">`;
      }
      // Category dropdown
      if (service.options.category) {
        html += `<label class="small-label" for="categorySelect">Category</label>`;
        html += `<select id="categorySelect" style="margin-bottom:8px;">`;
        html += `<option value="" disabled ${!svcObj.fields.category ? "selected" : ""}>-- Choose category --</option>`;
        SERVICE_CATEGORIES.forEach(cat => {
          html += `<option value="${cat}" ${svcObj.fields.category === cat ? "selected" : ""}>${cat}</option>`;
        });
        html += `</select>`;
        if (svcObj.fields.category === "Other") {
          html += `<input type="text" id="customCategoryInput" class="small-label" value="${svcObj.fields.customCategory || ""}" maxlength="40" placeholder="Custom category">`;
        }
      }
      // Complexity dropdown
      if (service.options.complexity) {
        html += `<label for="complexitySelect" class="small-label">Project Complexity</label>`;
        html += `<select id="complexitySelect" style="margin-bottom:8px;">`;
        html += `<option value="" disabled ${!svcObj.fields.complexity ? "selected" : ""}>-- Choose complexity --</option>`;
        PROJECT_COMPLEXITY_LEVELS.forEach(lvl => {
          html += `<option value="${lvl.val}" ${svcObj.fields.complexity === lvl.val ? "selected" : ""}>${lvl.label}</option>`;
        });
        html += `</select>`;
      }
      // Duration slider
      if (service.options.duration) {
        let val = svcObj.fields.duration || 1;
        html += `<div class="slider-row" id="durationSliderWrapper">
          <label for="durationSlider" class="small-label" style="margin-bottom:2px;">Duration:</label>
          <span style="font-size:0.85em;color:#aaa;">1</span>
          <input type="range" id="durationSlider" min="1" max="36" value="${val}">
          <span id="durationSliderValue" style="font-size:0.9em;color:#f39c12;font-weight:600;">${val}</span>
          <span style="font-size:0.85em;color:#aaa;">36 months</span>
        </div>`;
      }
      // Social Media Management platforms
      if (service.options.platforms) {
        html += `<label class="small-label">Select Platforms</label>`;
        html += `<div class="centered-checkboxes" id="smmPlatformsWrapper">`;
        ["Instagram","Facebook","LinkedIn","Other"].forEach(platform => {
          let checked = Array.isArray(svcObj.fields.platforms) && svcObj.fields.platforms.includes(platform) ? "checked" : "";
          html += `<label><input type="checkbox" class="smmPlatform" value="${platform}" ${checked}> ${platform}</label>`;
        });
        html += `</div>`;
        // If Other selected, show popup to enter platform name
        if (Array.isArray(svcObj.fields.platforms) && svcObj.fields.platforms.includes("Other") && svcObj.fields.otherPlatform) {
          html += `<div class="small-note" style="color:#e74c3c;">Other platform: ${svcObj.fields.otherPlatform}</div>`;
        }
      }
      // SEO Services type
      if (service.options.seoType) {
        html += `<label class="small-label">SEO Options</label>`;
        html += `<div class="centered-checkboxes" id="seoTypeWrapper">`;
        ["On-page SEO","Off-page SEO","Both"].forEach(opt => {
          let checked = Array.isArray(svcObj.fields.seoType) && svcObj.fields.seoType.includes(opt) ? "checked" : "";
          let disabled = (opt === "Off-page SEO" && !(svcObj.fields.seoType||[]).includes("On-page SEO")) ? "disabled" : "";
          html += `<label><input type="checkbox" class="seoType" value="${opt}" ${checked} ${disabled}> ${opt}</label>`;
        });
        html += `</div>`;
      }
      // E-commerce Store type
      if (service.options.ecommerceType) {
        html += `<label class="small-label">Store Platform</label>`;
        html += `<select id="ecommerceTypeSelect" style="margin-bottom:8px;">`;
        ["Shopify","WooCommerce","Odoo","Other"].forEach(opt => {
          html += `<option value="${opt}" ${svcObj.fields.ecommerceType===opt?"selected":""}>${opt}</option>`;
        });
        html += `</select>`;
        if (svcObj.fields.ecommerceType === "Other") {
          html += `<div class="small-note" style="color:#e74c3c;">Please request this service via WhatsApp.</div>`;
        }
      }
      // Marketplace Management platforms
      if (service.options.marketplacePlatforms) {
        html += `<label class="small-label">Select Marketplace Platforms</label>`;
        html += `<div class="centered-checkboxes" id="marketplacePlatformsWrapper">`;
        ["Amazon","Flipkart","Other"].forEach(opt => {
          let checked = Array.isArray(svcObj.fields.marketplacePlatforms) && svcObj.fields.marketplacePlatforms.includes(opt) ? "checked" : "";
          html += `<label><input type="checkbox" class="marketplacePlatform" value="${opt}" ${checked}> ${opt}</label>`;
        });
        html += `</div>`;
        if (Array.isArray(svcObj.fields.marketplacePlatforms) && svcObj.fields.marketplacePlatforms.includes("Other") && svcObj.fields.otherMarketplace) {
          html += `<div class="small-note" style="color:#e74c3c;">Other platform: ${svcObj.fields.otherMarketplace}</div>`;
        }
      }
      // Product count
      if (service.options.productCount) {
        let val = svcObj.fields.productCount || 1;
        html += `<label class="small-label" for="productCount">Number of Products</label>`;
        html += `<input type="number" id="productCount" min="1" max="10000" value="${val}">`;
      }
      // Branding Medium
      if (service.options.brandingMedium) {
        html += `<label class="small-label" for="brandingMediumSelect">Branding Medium</label>`;
        html += `<select id="brandingMediumSelect" style="margin-bottom:8px;">`;
        ["Online","Offline","Both"].forEach(opt => {
          html += `<option value="${opt}" ${svcObj.fields.brandingMedium===opt?"selected":""}>${opt}</option>`;
        });
        html += `</select>`;
      }
      // Instagram Followers
      if (service.options.followers) {
        let val = svcObj.fields.followers || 50;
        html += `<label class="small-label" for="followersCount">Instagram Followers (multiples of 50)</label>`;
        html += `<input type="number" id="followersCount" min="50" step="50" value="${val}">`;
      }
      // Meta and Google Ads
      if (service.options.adsType) {
        html += `<label class="small-label">Select Ads Platform</label>`;
        html += `<div class="centered-checkboxes" id="adsTypeWrapper">`;
        ["Meta Ads","Google Ads","Both"].forEach(opt => {
          let checked = Array.isArray(svcObj.fields.adsType) && svcObj.fields.adsType.includes(opt) ? "checked" : "";
          html += `<label><input type="checkbox" class="adsType" value="${opt}" ${checked}> ${opt}</label>`;
        });
        html += `</div>`;
      }
      if (service.options.campaignObjective) {
        html += `<label class="small-label">Campaign Objective</label>`;
        html += `<select id="campaignObjectiveSelect" style="margin-bottom:8px;">`;
        ["Sales","Leads","Traffic","Engagement","Awareness"].forEach(opt => {
          html += `<option value="${opt}" ${svcObj.fields.campaignObjective===opt?"selected":""}>${opt}</option>`;
        });
        html += `</select>`;
      }
      if (service.options.marketingBudget) {
        let val = svcObj.fields.marketingBudget || "";
        html += `<label class="small-label" for="marketingBudgetInput">Marketing Budget (₹)</label>`;
        html += `<input type="number" id="marketingBudgetInput" min="1000" placeholder="Enter amount" value="${val}">`;
      }
      // 3D or Product Design
      if (service.options.productName) {
        html += `<label class="small-label" for="productNameInput">Product Name</label>`;
        html += `<input type="text" id="productNameInput" maxlength="40" value="${svcObj.fields.productName||""}">`;
      }
      if (service.options.productCategory) {
        html += `<label class="small-label" for="productCategoryInput">Product Category</label>`;
        html += `<input type="text" id="productCategoryInput" maxlength="40" value="${svcObj.fields.productCategory||""}">`;
      }
    }
    $serviceFormSection.innerHTML = html;

    // Add listeners for all fields
    document.getElementById("serviceSelectMain").onchange = e => {
      svcObj.serviceKey = e.target.value;
      svcObj.fields = {};
      renderServiceForm(currentServiceId);
      renderPriceRange();
      hideCallNowCard();
    };
    if (document.getElementById("addServiceBtn")) {
      document.getElementById("addServiceBtn").onclick = () => {
        saveCurrentFormFields();
        addNewService();
      };
    }
    if (selectedKey) {
      // Save fields on change
      if (document.getElementById("industryField")) {
        document.getElementById("industryField").oninput = e => {
          svcObj.fields.industry = e.target.value;
        };
      }
      if (document.getElementById("categorySelect")) {
        document.getElementById("categorySelect").onchange = e => {
          svcObj.fields.category = e.target.value;
          if (e.target.value !== "Other") delete svcObj.fields.customCategory;
          renderServiceForm(currentServiceId);
        };
      }
      if (document.getElementById("customCategoryInput")) {
        document.getElementById("customCategoryInput").oninput = e => {
          svcObj.fields.customCategory = e.target.value;
        };
      }
      if (document.getElementById("complexitySelect")) {
        document.getElementById("complexitySelect").onchange = e => {
          svcObj.fields.complexity = e.target.value;
        };
      }
      if (document.getElementById("durationSlider")) {
        let slider = document.getElementById("durationSlider");
        let sliderVal = document.getElementById("durationSliderValue");
        slider.oninput = e => {
          sliderVal.textContent = e.target.value;
          svcObj.fields.duration = parseInt(e.target.value);
          renderPriceRange();
        };
      }
      if (document.getElementById("smmPlatformsWrapper")) {
        document.querySelectorAll(".smmPlatform").forEach(cb => {
          cb.onchange = e => {
            let arr = Array.from(document.querySelectorAll(".smmPlatform:checked")).map(x=>x.value);
            svcObj.fields.platforms = arr;
            // If Other checked, show popup
            if (arr.includes("Other")) {
              showOtherPlatformPopup("smm", val => {
                svcObj.fields.otherPlatform = val;
                renderServiceForm(currentServiceId);
              }, svcObj.fields.otherPlatform||"");
            } else {
              delete svcObj.fields.otherPlatform;
            }
            renderServiceForm(currentServiceId);
            renderPriceRange();
          };
        });
      }
      if (document.getElementById("seoTypeWrapper")) {
        document.querySelectorAll(".seoType").forEach(cb => {
          cb.onchange = e => {
            let arr = Array.from(document.querySelectorAll(".seoType:checked")).map(x=>x.value);
            svcObj.fields.seoType = arr;
            renderServiceForm(currentServiceId);
            renderPriceRange();
          };
        });
      }
      if (document.getElementById("ecommerceTypeSelect")) {
        document.getElementById("ecommerceTypeSelect").onchange = e => {
          svcObj.fields.ecommerceType = e.target.value;
          renderServiceForm(currentServiceId);
          renderPriceRange();
        };
      }
      if (document.getElementById("marketplacePlatformsWrapper")) {
        document.querySelectorAll(".marketplacePlatform").forEach(cb => {
          cb.onchange = e => {
            let arr = Array.from(document.querySelectorAll(".marketplacePlatform:checked")).map(x=>x.value);
            svcObj.fields.marketplacePlatforms = arr;
            if (arr.includes("Other")) {
              showOtherPlatformPopup("marketplace", val => {
                svcObj.fields.otherMarketplace = val;
                renderServiceForm(currentServiceId);
              }, svcObj.fields.otherMarketplace||"");
            } else {
              delete svcObj.fields.otherMarketplace;
            }
            renderServiceForm(currentServiceId);
            renderPriceRange();
          };
        });
      }
      if (document.getElementById("productCount")) {
        document.getElementById("productCount").oninput = e => {
          svcObj.fields.productCount = parseInt(e.target.value);
          renderPriceRange();
        };
      }
      if (document.getElementById("brandingMediumSelect")) {
        document.getElementById("brandingMediumSelect").onchange = e => {
          svcObj.fields.brandingMedium = e.target.value;
        };
      }
      if (document.getElementById("followersCount")) {
        document.getElementById("followersCount").oninput = e => {
          svcObj.fields.followers = parseInt(e.target.value);
          renderPriceRange();
        };
      }
      if (document.getElementById("adsTypeWrapper")) {
        document.querySelectorAll(".adsType").forEach(cb => {
          cb.onchange = e => {
            let arr = Array.from(document.querySelectorAll(".adsType:checked")).map(x=>x.value);
            svcObj.fields.adsType = arr;
            renderPriceRange();
          };
        });
      }
      if (document.getElementById("campaignObjectiveSelect")) {
        document.getElementById("campaignObjectiveSelect").onchange = e => {
          svcObj.fields.campaignObjective = e.target.value;
        };
      }
      if (document.getElementById("marketingBudgetInput")) {
        document.getElementById("marketingBudgetInput").oninput = e => {
          svcObj.fields.marketingBudget = parseInt(e.target.value);
          renderPriceRange();
        };
      }
      if (document.getElementById("productNameInput")) {
        document.getElementById("productNameInput").oninput = e => {
          svcObj.fields.productName = e.target.value;
        };
      }
      if (document.getElementById("productCategoryInput")) {
        document.getElementById("productCategoryInput").oninput = e => {
          svcObj.fields.productCategory = e.target.value;
        };
      }
    }
    // Save to state
    let idx = multiServiceArr.findIndex(s => s.id === svcObj.id);
    if (idx === -1) multiServiceArr.push(svcObj);
    else multiServiceArr[idx] = svcObj;
    renderMultiServiceList();
    renderPriceRange();
    hideCallNowCard();
    // If "Other" service, show call now card
    if (selectedKey === "Other" || (selectedKey === "eCommerce Store" && svcObj.fields.ecommerceType === "Other")) {
      showCallNowCard();
    }
  }

  function saveCurrentFormFields() {
    // Save all fields of current form to multiServiceArr
    // (already done in event handlers)
  }

  function addNewService() {
    // Save current, then add new blank
    renderServiceForm(null);
  }

  window.arEditService = function(id) {
    renderServiceForm(id);
  };
  window.arRemoveService = function(id) {
    if (multiServiceArr.length <= 1) {
      // Always keep at least one service
      multiServiceArr = [];
      renderServiceForm(null);
    } else {
      let idx = multiServiceArr.findIndex(s => s.id === id);
      if (idx > -1) multiServiceArr.splice(idx, 1);
      renderMultiServiceList();
      renderServiceForm(multiServiceArr.length > 0 ? multiServiceArr[0].id : null);
    }
    renderPriceRange();
    hideCallNowCard();
  };

  // --- Price Range Display ---
  function renderPriceRange() {
    // For all services, show price range
    let totalMin = 0, totalMax = 0, totalAvg = 0, n = 0;
    let priceSummary = "";
    let hasOther = false;
    for (let svc of multiServiceArr) {
      let service = getServiceByKey(svc.serviceKey);
      if (!service) continue;
      if (svc.serviceKey === "Other" || (svc.serviceKey === "eCommerce Store" && svc.fields.ecommerceType === "Other")) {
        hasOther = true;
        continue;
      }
      let {min, max, avg} = getServicePrice(svc);
      totalMin += min;
      totalMax += max;
      totalAvg += avg;
      n++;
      priceSummary += `${service.label}: ₹${min.toLocaleString()} - ₹${max.toLocaleString()} (avg ₹${avg.toLocaleString()})\n`;
    }
    if (hasOther) priceSummary += "Other: Please request quote via WhatsApp.\n";
    $estimatedPriceRange.innerHTML = priceSummary ? priceSummary.replace(/\n/g,"<br>") : "";
    $averagePriceRange.innerHTML = n ? `Average total: ₹${Math.round(totalAvg).toLocaleString()}` : "";
  }

  // --- Service Price Calculation ---
  function getServicePrice(svcObj) {
    let service = getServiceByKey(svcObj.serviceKey);
    if (!service) return {min:0,max:0,avg:0};
    let min = service.min, max = service.max, avg = service.avg;
    // Custom logic per service
    if (service.key === "Logo Design") {
      min = max = avg = 4000;
    }
    if (service.key === "Social Media Management") {
      // Each platform
      let platforms = svcObj.fields.platforms || [];
      let platSum = 0;
      platforms.forEach(p => {
        if (p === "Instagram") platSum += 8999;
        else if (p === "Facebook") platSum += 7999;
        else if (p === "LinkedIn") platSum += 11999;
        else platSum += 0;
      });
      let duration = svcObj.fields.duration || 1;
      min = max = avg = platSum * duration;
    }
    if (service.key === "SEO Services") {
      let types = svcObj.fields.seoType || [];
      if (types.includes("Both")) min = max = avg = 14000;
      else if (types.includes("On-page SEO") && types.includes("Off-page SEO")) min = max = avg = 14000;
      else if (types.includes("On-page SEO")) min = max = avg = 9000;
      else if (types.includes("Off-page SEO")) min = max = avg = 5000;
      else min = max = avg = 0;
    }
    if (service.key === "eCommerce Store") {
      let type = svcObj.fields.ecommerceType;
      if (type === "Shopify") min = max = avg = 33250;
      else if (type === "WooCommerce") min = max = avg = 49800;
      else if (type === "Odoo") min = max = avg = 41600;
      else if (type === "Other") min = max = avg = 0;
    }
    if (service.key === "Marketplace Management") {
      let platforms = svcObj.fields.marketplacePlatforms || [];
      let nPlatforms = platforms.length || 1;
      let nProducts = svcObj.fields.productCount || 1;
      min = max = avg = 8000 * nPlatforms + 100 * nProducts;
    }
    if (service.key === "Instagram Followers") {
      let n = svcObj.fields.followers || 50;
      min = max = avg = Math.round(n * 10);
    }
    if (service.key === "Meta and Google Ads") {
      let budget = svcObj.fields.marketingBudget || 0;
      if (budget <= 25000) min = max = avg = Math.round(budget * 0.2);
      else min = max = avg = Math.round(budget * 0.35);
    }
    if (service.key === "3D or Product Design") {
      let n = svcObj.fields.productCount || 1;
      min = max = avg = n * 6000;
    }
    // Duration multiplier
    if (service.options.duration && service.key !== "Social Media Management") {
      let months = svcObj.fields.duration || 1;
      min *= months; max *= months; avg *= months;
    }
    // Bulk discount if total > 25,000
    // (handled in preview)
    return {min,max,avg};
  }

  // --- Call Now Card ---
  function showCallNowCard() {
    if (callNowCardVisible) return;
    $callNowCardContainer.innerHTML = `
      <div class="call-now-card" id="callNowCard">
        <button class="close-call-card" type="button" aria-label="Close" onclick="window.arCloseCallNowCard()">&times;</button>
        <div>Please request this service via WhatsApp using the button below.</div>
        <a class="call-btn" href="tel:+919991283530" target="_blank" rel="noopener">Call Now</a>
      </div>
    `;
    callNowCardVisible = true;
    // Hide quotation preview button
    $previewQuotationBtn.style.display = "none";
  }
  function hideCallNowCard() {
    $callNowCardContainer.innerHTML = "";
    callNowCardVisible = false;
    $previewQuotationBtn.style.display = "";
  }
  window.arCloseCallNowCard = function() {
    hideCallNowCard();
  };

  // --- Other Platform Popup ---
  function showOtherPlatformPopup(type, cb, initialVal) {
    $otherPlatformPopupContent.innerHTML = `
      <div>
        <label class="small-label" for="otherPlatformInput">Enter Platform Name</label>
        <input type="text" id="otherPlatformInput" maxlength="30" value="${initialVal||""}">
        <button class="small-btn" id="otherPlatformSubmitBtn" type="button">Submit</button>
      </div>
    `;
    $otherPlatformPopup.classList.remove("hidden");
    document.body.style.overflow = "hidden";
    document.getElementById("otherPlatformSubmitBtn").onclick = () => {
      let val = document.getElementById("otherPlatformInput").value.trim();
      if (val) {
        cb(val);
        $otherPlatformPopup.classList.add("hidden");
        document.body.style.overflow = "";
      }
    };
    document.querySelector("#otherPlatformPopup .close-other-popup").onclick = () => {
      $otherPlatformPopup.classList.add("hidden");
      document.body.style.overflow = "";
    };
  }

  // --- Quotation Preview ---
  function showQuotationPreview() {
    // Save user details if not present
    if (!userDetails) {
      showUserDetailsPopup(() => showQuotationPreview());
      return;
    }
    // Hide if "Other" service
    let hasOther = multiServiceArr.some(svc => svc.serviceKey === "Other" || (svc.serviceKey === "eCommerce Store" && svc.fields.ecommerceType === "Other"));
    if (hasOther) return;
    // Prepare preview
    $quotePreviewSection.classList.remove("hidden");
    document.body.style.overflow = "hidden";
    // Build table
    let total = 0, avgTotal = 0, discount = 0;
    let rows = '';
    for (let svc of multiServiceArr) {
      let service = getServiceByKey(svc.serviceKey);
      if (!service) continue;
      let {min, max, avg} = getServicePrice(svc);
      avgTotal += avg;
      let desc = service.desc || "";
      // Details (platforms, duration, etc)
      let details = '';
      if (service.options.platforms && Array.isArray(svc.fields.platforms)) {
        details += "Platforms: " + svc.fields.platforms.join(", ");
        if (svc.fields.otherPlatform) details += ` (${svc.fields.otherPlatform})`;
      }
      if (service.options.duration && svc.fields.duration) {
        details += (details?", ":"") + `Duration: ${svc.fields.duration} month(s)`;
      }
      if (service.options.productCount && svc.fields.productCount) {
        details += (details?", ":"") + `Products: ${svc.fields.productCount}`;
      }
      if (service.options.seoType && Array.isArray(svc.fields.seoType)) {
        details += (details?", ":"") + `SEO: ${svc.fields.seoType.join(", ")}`;
      }
      if (service.options.ecommerceType && svc.fields.ecommerceType) {
        details += (details?", ":"") + `Platform: ${svc.fields.ecommerceType}`;
      }
      if (service.options.marketplacePlatforms && Array.isArray(svc.fields.marketplacePlatforms)) {
        details += (details?", ":"") + `Marketplaces: ${svc.fields.marketplacePlatforms.join(", ")}`;
        if (svc.fields.otherMarketplace) details += ` (${svc.fields.otherMarketplace})`;
      }
      if (service.options.brandingMedium && svc.fields.brandingMedium) {
        details += (details?", ":"") + `Medium: ${svc.fields.brandingMedium}`;
      }
      if (service.options.followers && svc.fields.followers) {
        details += (details?", ":"") + `Followers: ${svc.fields.followers}`;
      }
      if (service.options.adsType && Array.isArray(svc.fields.adsType)) {
        details += (details?", ":"") + `Ads: ${svc.fields.adsType.join(", ")}`;
      }
      if (service.options.campaignObjective && svc.fields.campaignObjective) {
        details += (details?", ":"") + `Objective: ${svc.fields.campaignObjective}`;
      }
      if (service.options.marketingBudget && svc.fields.marketingBudget) {
        details += (details?", ":"") + `Budget: ₹${svc.fields.marketingBudget}`;
      }
      if (service.options.productName && svc.fields.productName) {
        details += (details?", ":"") + `Product: ${svc.fields.productName}`;
      }
      if (service.options.productCategory && svc.fields.productCategory) {
        details += (details?", ":"") + `Category: ${svc.fields.productCategory}`;
      }
      if (service.options.industry && svc.fields.industry) {
        details += (details?", ":"") + `Industry: ${svc.fields.industry}`;
      }
      if (service.options.complexity && svc.fields.complexity) {
        details += (details?", ":"") + `Complexity: ${svc.fields.complexity}`;
      }
      if (service.options.category && svc.fields.category) {
        let cat = svc.fields.category;
        if (cat === "Other" && svc.fields.customCategory) cat += ` (${svc.fields.customCategory})`;
        details += (details?", ":"") + `Category: ${cat}`;
      }
      rows += `<tr>
        <td class="left">${service.label}</td>
        <td class="left">${desc}</td>
        <td class="left">${details}</td>
        <td>₹${min.toLocaleString()}</td>
        <td>₹${max.toLocaleString()}</td>
        <td>₹${avg.toLocaleString()}</td>
      </tr>`;
      total += min;
    }
    // Bulk discount
    if (avgTotal > 25000) {
      discount = Math.round(avgTotal * 0.08); // 8% discount
      avgTotal -= discount;
    }
    // Build preview
    $quotePreviewContent.innerHTML = `
      <div class="quotation-header">
        <img src="${COMPANY.logo}" alt="AfterResult Logo">
        <div>
          <div style="font-weight:700; font-size:1.1em;">${COMPANY.name}</div>
          <div style="font-size:11px;">${COMPANY.address}</div>
        </div>
      </div>
      <div class="quotation-meta">
        <div><b>Date:</b> ${new Date().toLocaleDateString()}</div>
        <div><b>To:</b> ${userDetails.name} (${userDetails.email}, ${userDetails.phone})</div>
      </div>
      <div class="quotation-section-title">Quotation Details</div>
      <table class="quotation-table">
        <thead>
          <tr>
            <th>Service</th>
            <th>Description</th>
            <th>Details</th>
            <th>Min Price</th>
            <th>Max Price</th>
            <th>Average</th>
          </tr>
        </thead>
        <tbody>
          ${rows}
        </tbody>
      </table>
      <div class="quotation-section-title">Summary</div>
      <div>
        <b>Total (average):</b> ₹${avgTotal.toLocaleString()}<br>
        ${discount ? `<span style="color:#e74c3c;">Bulk Discount Applied: -₹${discount.toLocaleString()}</span><br>` : ""}
        <span style="font-size:12px;color:#888;">Actual prices may vary slightly. Final invoice shared by the company will reflect the correct price.</span>
      </div>
      <div class="quotation-sign">
        <br>Regards,<br>
        <b>${COMPANY.executive}</b><br>
        ${COMPANY.designation}<br>
        <a href="mailto:${COMPANY.email}" style="color:#1d6fa5;">${COMPANY.email}</a><br>
        <a href="tel:${COMPANY.phone.replace(/\s/g,'')}" style="color:#1d6fa5;">${COMPANY.phone}</a>
      </div>
      <div class="qr-section">
        <img src="${COMPANY.qr}" alt="QR">
        <a href="${COMPANY.website}" target="_blank" class="website-link">${COMPANY.website}</a>
      </div>
    `;
    lastPreviewedServiceIds = multiServiceArr.map(s=>s.id);
  }

  function hideQuotationPreview() {
    $quotePreviewSection.classList.add("hidden");
    document.body.style.overflow = "";
  }

  // --- User Details Popup ---
  function showUserDetailsPopup(cb) {
    $popupFormOverlay.classList.add("show");
    if (userDetails) {
      $popupForm.userName.value = userDetails.name;
      $popupForm.userPhone.value = userDetails.phone;
      $popupForm.userEmail.value = userDetails.email;
      $popupForm.userCompany.value = userDetails.company||"";
    } else {
      $popupForm.userName.value = "";
      $popupForm.userPhone.value = "";
      $popupForm.userEmail.value = "";
      $popupForm.userCompany.value = "";
    }
    $popupForm.onsubmit = e => {
      e.preventDefault();
      let name = $popupForm.userName.value.trim();
      let phone = $popupForm.userPhone.value.trim();
      let email = $popupForm.userEmail.value.trim();
      let company = $popupForm.userCompany.value.trim();
      if (!name || !phone || !email) return;
      userDetails = { name, phone, email, company };
      if (window.localStorage) localStorage.setItem("ar_user_details", JSON.stringify(userDetails));
      $popupFormOverlay.classList.remove("show");
      if (typeof cb === "function") cb();
    };
    $popupCancelBtn.onclick = () => {
      $popupFormOverlay.classList.remove("show");
    };
  }

  // --- WhatsApp Quotation ---
  function sendQuotationViaWhatsApp() {
    // If "Other" service, open WhatsApp with message
    let hasOther = multiServiceArr.some(svc => svc.serviceKey === "Other" || (svc.serviceKey === "eCommerce Store" && svc.fields.ecommerceType === "Other"));
    let msg = "";
    if (!userDetails) {
      showUserDetailsPopup(() => sendQuotationViaWhatsApp());
      return;
    }
    msg += `Name: ${userDetails.name}\nEmail: ${userDetails.email}\nPhone: ${userDetails.phone}\nCompany: ${userDetails.company||""}\n\n`;
    msg += "Quotation Request:\n";
    multiServiceArr.forEach(svc => {
      let service = getServiceByKey(svc.serviceKey);
      if (!service) return;
      msg += `Service: ${service.label}\n`;
      msg += `Description: ${service.desc}\n`;
      Object.keys(svc.fields).forEach(fld => {
        msg += `${fld}: ${svc.fields[fld]}\n`;
      });
      msg += "\n";
    });
    if (hasOther) {
      msg += "Requesting quotation for a custom service.\n";
    }
    let url = "https://wa.me/919599169901?text=" + encodeURIComponent(msg);
    window.open(url,"_blank");
  }

  // --- Download Quotation as PDF ---
  $downloadQuoteBtn.onclick = async function() {
    $downloadQuoteBtn.disabled = true;
    $downloadQuoteBtn.textContent = "Generating PDF...";
    let node = $quotePreviewSection;
    html2canvas(node, {scale:2, backgroundColor:"#fff"}).then(canvas => {
      let imgData = canvas.toDataURL("image/png");
      let pdf = new window.jspdf.jsPDF("p","mm","a4");
      let pageWidth = pdf.internal.pageSize.getWidth();
      let pageHeight = pdf.internal.pageSize.getHeight();
      let imgProps = pdf.getImageProperties(imgData);
      let pdfWidth = pageWidth - 20;
      let pdfHeight = (imgProps.height * pdfWidth) / imgProps.width;
      pdf.addImage(imgData, "PNG", 10, 10, pdfWidth, pdfHeight);
      pdf.save("AfterResult-Quotation.pdf");
      $downloadQuoteBtn.disabled = false;
      $downloadQuoteBtn.textContent = "Download Quotation as PDF";
    });
  };

  // --- Event Listeners ---
  $previewQuotationBtn.onclick = function() {
    saveCurrentFormFields();
    showQuotationPreview();
  };
  $closePreviewBtn.onclick = function() {
    hideQuotationPreview();
  };
  $whatsappQuotationBtn.onclick = function() {
    saveCurrentFormFields();
    sendQuotationViaWhatsApp();
  };

  // --- Auto-Hide Quotation Preview ---
  document.addEventListener("click", function(e) {
    if (!$quotePreviewSection.classList.contains("hidden")) {
      // If user clicks outside preview or selects another service
      if (!e.target.closest("#quotePreviewSection") && !e.target.closest("#previewQuotationBtn")) {
        hideQuotationPreview();
      }
    }
  });

  // --- INIT UI ---
  if (multiServiceArr.length === 0) {
    multiServiceArr.push({id:"svc1",serviceKey:"",fields:{}});
  }
  renderServiceForm(multiServiceArr[0].id);

})();
</script>
