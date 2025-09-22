<!--
AfterResult Quotation Estimator Widget
This is a self-contained HTML+CSS+JS widget for Markdown/HTML pages.
-->

<style>
/* Place your CSS here. Keep it in the Markdown for widget isolation. */
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
    <button id="downloadQuoteBtn" type="button" style="margin-top: 10px; background: #222; color: #f39c12; border: none; padding: 8px 14px; border-radius: 20px; font-size: 12px; cursor: pointer;">Download Quotation</button>
    <button id="closePreviewBtn" type="button" style="margin-top: 10px; background: #222; color: #f39c12; border: none; padding: 8px 14px; border-radius: 20px; font-size: 12px; cursor: pointer;">Close</button>
  </div>
  <div id="callNowCardContainer"></div>
</div>
<div id="popupFormOverlay" role="dialog" aria-modal="true" aria-labelledby="popupFormTitle" style="position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.85); display: none; justify-content: center; align-items: center; z-index: 10000;">
  <form id="popupForm" novalidate style="background: #222; padding: 20px 25px; border-radius: 15px; max-width: 400px; width: 90%; box-sizing: border-box; box-shadow: 0 0 15px #f39c12;">
    <h3 id="popupFormTitle" style="color:#f39c12; margin-top:0; margin-bottom:15px; font-weight:400; text-align:center;">Please Enter Your Details</h3>
    <label for="userName">Name *</label>
    <input type="text" id="userName" name="userName" required autocomplete="name">
    <label for="userPhone">Phone Number *</label>
    <input type="tel" id="userPhone" name="userPhone" pattern="^\+?\d{7,15}$" placeholder="+919999999999" required autocomplete="tel">
    <label for="userEmail">Email *</label>
    <input type="email" id="userEmail" name="userEmail" required autocomplete="email">
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

<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js" defer></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js" defer></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrious/4.0.2/qrious.min.js" defer></script>
<script>
(function () {
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

  // Service definitions, categories, descriptions, etc. (same as your code)
  // ...

  // --- STATE ---
  let multiServiceArr = [];
  let serviceCounter = 1;
  let currentServiceId = null;
  let userDetails = null;
  let lastPreviewedServiceIds = [];
  let otherPlatformPopupState = null;
  let callNowCardVisible = false;

  // --- INIT: Load user details from localStorage ---
  if (typeof window !== "undefined" && window.localStorage) {
    try {
      userDetails = JSON.parse(localStorage.getItem("ar_user_details") || "null");
    } catch (e) { userDetails = null; }
  }

  // --- DOM cache (with guards!) ---
  function getEl(id) { return document.getElementById(id); }
  const $serviceFormSection = getEl("serviceFormSection");
  const $multiServiceList = getEl("multiServiceList");
  const $estimatedPriceRange = getEl("estimatedPriceRange");
  const $averagePriceRange = getEl("averagePriceRange");
  const $previewQuotationBtn = getEl("previewQuotationBtn");
  const $whatsappQuotationBtn = getEl("whatsappQuotationBtn");
  const $quotePreviewSection = getEl("quotePreviewSection");
  const $quotePreviewContent = getEl("quotePreviewContent");
  const $downloadQuoteBtn = getEl("downloadQuoteBtn");
  const $closePreviewBtn = getEl("closePreviewBtn");
  const $popupFormOverlay = getEl("popupFormOverlay");
  const $popupForm = getEl("popupForm");
  const $popupCancelBtn = getEl("popupCancelBtn");
  const $callNowCardContainer = getEl("callNowCardContainer");
  const $otherPlatformPopup = getEl("otherPlatformPopup");
  const $otherPlatformPopupContent = getEl("otherPlatformPopupContent");

  // --- JS Disabled Message ---
  if (getEl("calculatorContainer")) {
    getEl("calculatorContainer").insertAdjacentHTML(
      "beforebegin",
      "<noscript><div style='color:#e74c3c;background:#222;padding:10px;border-radius:8px;text-align:center;margin-bottom:12px;'>Please enable JavaScript to use the Quotation Estimator.</div></noscript>"
    );
  }

  // --- Example: Render minimal form on load (prevent null errors) ---
  function renderMultiServiceList() {
    if ($multiServiceList) $multiServiceList.innerHTML = '';
  }
  function renderServiceForm() {
    if ($serviceFormSection) $serviceFormSection.innerHTML = '<div style="color:#aaa;">[Estimator form appears here]</div>';
  }

  function init() {
    renderMultiServiceList();
    renderServiceForm();
    // Setup event listeners only if elements exist
    if ($previewQuotationBtn) $previewQuotationBtn.addEventListener("click", function(){});
    if ($whatsappQuotationBtn) $whatsappQuotationBtn.addEventListener("click", function(){});
    if ($downloadQuoteBtn) $downloadQuoteBtn.addEventListener("click", function(){});
    if ($closePreviewBtn) $closePreviewBtn.addEventListener("click", function(){});
    if ($popupCancelBtn) $popupCancelBtn.addEventListener("click", function(){});
  }

  if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", init);
  } else {
    init();
  }
})();
</script>
