<html>
  <body>
    <script>
      var FIRST_NAME = "Maria";
      var LAST_NAME = "Souza";
      var EMAIL = "maria@test.com";
      var PHONE = "987654312";

      var CLIENT_ID = "1a2b3c4d76";
      var COUNTRY_OF_CARD = "Brazil";
      var BANK_NAME = "VISA";
	
	  var BIN_NUMBER = "2345678901";
      var BIN_NUMBER_MASKED = BIN_NUMBER.slice(0, -4) + "****";		
	
      window.addEventListener("onEmbeddedMessagingReady", function (e) {

		const fetchBrowserInfo = () => {
			const ua = navigator.userAgent;
			let name = "Unknown";
			let version = "";

			if (ua.includes("OPR") || ua.includes("Opera")) {
				name = "Opera";
				version = ua.match(/OPR\/([\d.]+)/)?.[1] || ua.match(/Opera\/([\d.]+)/)?.[1];
			} else if (ua.includes("Edg")) {
				name = "Edge";
				version = ua.match(/Edg\/([\d.]+)/)?.[1];
			} else if (ua.includes("Chrome") && !ua.includes("Edg") && !ua.includes("OPR")) {
				name = "Chrome";
				version = ua.match(/Chrome\/([\d.]+)/)?.[1];
			} else if (ua.includes("Safari") && !ua.includes("Chrome")) {
				name = "Safari";
				version = ua.match(/Version\/([\d.]+)/)?.[1];
			} else if (ua.includes("Firefox")) {
				name = "Firefox";
				version = ua.match(/Firefox\/([\d.]+)/)?.[1];
			}

			return `${name} ${version}`;
		};

		const browserInfo = fetchBrowserInfo();
		const browserLanguage = navigator.language;
		const browserPlatform = navigator.platform;

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
		  "X10_first_digits_of_the_Card" : BIN_NUMBER

        });
      });

      function initEmbeddedMessaging() {
        try {

			//let browserLanguage = navigator.language || navigator.userLanguage || 'en-US';
			//console.log('First Information:', browserLanguage);
			//let supportedLanguages = ['en-US', 'es', 'pt-BR'];
			//let finalLanguage = supportedLanguages.includes(browserLanguage) ? browserLanguage : 'en-US';
			//console.log('Final language to use:', finalLanguage);
			//embeddedservice_bootstrap.settings.language = finalLanguage;

			var LANGUAGE = 'Spanish';
			var languageMap = {
			'Portuguese': 'pt-BR',
			'Spanish': 'es',
			'English': 'en-US'
			};
			var finalLanguage = languageMap[LANGUAGE] || 'en-US';
			embeddedservice_bootstrap.settings.language = finalLanguage;
			console.log('Idioma definido:', finalLanguage);			

			embeddedservice_bootstrap.init(
				'00DOx000002jjB7',
				'Amex',
				'https://axaus-travel--dev.sandbox.my.site.com/ESWAmex1754486075194',
				{
					scrt2URL: 'https://axaus-travel--dev.sandbox.my.salesforce-scrt.com'
				}
			);
		} catch (err) {
			console.error('Error loading Embedded Messaging: ', err);
		}
      }
    </script>

    <script type='text/javascript' src='https://axaus-travel--dev.sandbox.my.site.com/ESWAmex1754486075194/assets/js/bootstrap.min.js' onload='initEmbeddedMessaging()'></script>

  </body>
</html>
