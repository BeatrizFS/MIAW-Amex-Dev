<html>
  <body>
	<script>
	   var FIRST_NAME = "Marcela";
	   var LAST_NAME = "Lima";
	   var EMAIL = "marcela@test.com";
	   var PHONE = "987654333";

	   var CLIENT_ID = "1a2b3c4d78";
	   var COUNTRY_OF_CARD = "Brazil";
	   var BANK_NAME = "VISA";
	
	   var BIN_NUMBER = "2345678981";
	   var BIN_NUMBER_MASKED = BIN_NUMBER.slice(0, -4) + "****";		
	
		window.addEventListener("onEmbeddedMessagingReady", function (e) {

		const userAgent = navigator.userAgent;
		
		const fetchBrowserInfo = () => {
			let name = "Unknown";
			let version = "";

			if (userAgent.includes("OPR") || userAgent.includes("Opera")) {
				name = "Opera";
				version = userAgent.match(/OPR\/([\d.]+)/)?.[1] || userAgent.match(/Opera\/([\d.]+)/)?.[1];
			} else if (userAgent.includes("Edg")) {
				name = "Edge";
				version = userAgent.match(/Edg\/([\d.]+)/)?.[1];
			} else if (userAgent.includes("Chrome") && !userAgent.includes("Edg") && !userAgent.includes("OPR")) {
				name = "Chrome";
				version = userAgent.match(/Chrome\/([\d.]+)/)?.[1];
			} else if (userAgent.includes("Safari") && !userAgent.includes("Chrome")) {
				name = "Safari";
				version = userAgent.match(/Version\/([\d.]+)/)?.[1];
			} else if (userAgent.includes("Firefox")) {
				name = "Firefox";
				version = userAgent.match(/Firefox\/([\d.]+)/)?.[1];
			}

			return `${name} ${version}`;
		};

		const browserInfo = fetchBrowserInfo();
		const browserLanguage = navigator.language;
		const browserPlatform = navigator.platform;
		const screenResolution = `${window.screen.width}x${window.screen.height}`;

		embeddedservice_bootstrap.prechatAPI.setVisiblePrechatFields({
		  "_firstName": {
			"value": FIRST_NAME,
			"isEditableByEndUser": true
		  },
		  "_lastName": {
			"value": LAST_NAME,
			"isEditableByEndUser": true
		  },
		  "Bin_Number": {
			"value": BIN_NUMBER_MASKED,
			"isEditableByEndUser": true
		  }
		});
		
		embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
		  "Email" : EMAIL,
		  "Phone" : PHONE,
		  "Client_ID" : CLIENT_ID,
		  "Country_Of_Card" : COUNTRY_OF_CARD,
		  "Bank_Name" : BANK_NAME,
		  "BrowserName" : browserInfo,
		  "BrowserLanguage" : browserLanguage,
		  "BrowserPlatform" : browserPlatform,
		  "UserAgent" : userAgent,
		  "ScreenResolution" : screenResolution,
		  "X10_first_digits_of_the_Card" : BIN_NUMBER
				
		});
	  });
   
      function initEmbeddedMessaging() {
        try {

			let browserLanguage = navigator.language || navigator.userLanguage || 'en-US';
			console.log('First Information:', browserLanguage);
			let supportedLanguages = ['en-US', 'es', 'pt-BR'];
			let finalLanguage = supportedLanguages.includes(browserLanguage) ? browserLanguage : 'en-US';
			console.log('Final language to use:', finalLanguage);
			embeddedservice_bootstrap.settings.language = finalLanguage;

			embeddedservice_bootstrap.settings.language = finalLanguage;
			console.log('Idioma definido:', finalLanguage);			

			embeddedservice_bootstrap.init(
				'00DOx000002jjB7',
				'Amex_External_Website',
				'https://axaus-travel--dev.sandbox.my.site.com/ESWAmexExternalWebsite1756993093717',
				{
					scrt2URL: 'https://axaus-travel--dev.sandbox.my.salesforce-scrt.com'
				}
			);
        } catch (err) {
          console.error('Erro ao carregar Embedded Messaging:', err);
        }
      }
    </script>
	<script 
	type='text/javascript' 
	src='https://axaus-travel--dev.sandbox.my.site.com/ESWAmexExternalWebsite1756993093717/assets/js/bootstrap.min.js' 
	onload='initEmbeddedMessaging()'>
	</script>

  </body>
</html>
