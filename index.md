<script type='text/javascript'>
	function initEmbeddedMessaging() {
		try {
			embeddedservice_bootstrap.settings.language = 'en_US'; // For example, enter 'en' or 'en-US'

			embeddedservice_bootstrap.init(
				'00DOx000002jjB7',
				'Amex_External_Website',
				'https://axaus-travel--dev.sandbox.my.site.com/ESWAmexExternalWebsite1756993093717',
				{
					scrt2URL: 'https://axaus-travel--dev.sandbox.my.salesforce-scrt.com'
				}
			);
		} catch (err) {
			console.error('Error loading Embedded Messaging: ', err);
		}
	};
</script>
<script type='text/javascript' src='https://axaus-travel--dev.sandbox.my.site.com/ESWAmexExternalWebsite1756993093717/assets/js/bootstrap.min.js' onload='initEmbeddedMessaging()'></script>
