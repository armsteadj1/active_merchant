# Active Merchant

Active Merchant is an extraction from the e-commerce system [Shopify](http://www.shopify.com).
Shopify's requirements for a simple and unified API to access dozens of different payment
gateways with very different internal APIs was the chief principle in designing the library.

Active Merchant has been in production use since June 2006 and is now used in most modern
Ruby applications which deal with financial transactions.

It was developed for usage in Ruby on Rails web applications and integrates seamlessly
as a plugin but it also works excellently as a stand alone library.

See {file:GettingStarted.md} if you want to learn more about using Active Merchant in your
applications.

## Installation

### From Git

You can check out the latest source from git:

    git clone git://github.com/Shopify/active_merchant.git

### As a Rails plugin

ActiveMerchant includes an init.rb file. This means that Rails will automatically load ActiveMerchant on startup. Run
the following command from the root directory of your Rails project to install ActiveMerchant as a Rails plugin:

    script/plugin install git://github.com/Shopify/active_merchant.git

### From RubyGems

Installation from RubyGems

    gem install activemerchant

Alternatively, add the following to your Gemfile

    gem 'activemerchant', :require => 'active_merchant'

## Usage

This simple example demonstrates how a purchase can be made using a person's
credit card details.

	require 'rubygems'
	require 'active_merchant'
	
	# Use the TrustCommerce test servers
	ActiveMerchant::Billing::Base.mode = :test

	gateway = ActiveMerchant::Billing::TrustCommerceGateway.new(
	            :login => 'TestMerchant',
	            :password => 'password')
	
	# ActiveMerchant accepts all amounts as Integer values in cents
	amount = 1000  # $10.00
	
	# The card verification value is also known as CVV2, CVC2, or CID 
	credit_card = ActiveMerchant::Billing::CreditCard.new(
	                :first_name         => 'Bob',
	                :last_name          => 'Bobsen',
	                :number             => '4242424242424242',
	                :month              => '8',
	                :year               => '2012',
	                :verification_value => '123')
	
	# Validating the card automatically detects the card type
	if credit_card.valid?
	  # Capture $10 from the credit card
	  response = gateway.purchase(amount, credit_card)
	
	  if response.success?
	    puts "Successfully charged $#{sprintf("%.2f", amount / 100)} to the credit card #{credit_card.display_number}"
	  else
	    raise StandardError, response.message 
	  end
	end

For more in-depth documentation and tutorials, see {file:GettingStarted.md} and the
[API documentation](http://rubydoc.info/github/Shopify/active_merchant/master/file/README.md).

## Supported Direct Payment Gateways

The [ActiveMerchant Wiki](http://github.com/Shopify/active_merchant/wikis) contains a [table of features supported by each gateway](http://github.com/Shopify/active_merchant/wikis/gatewayfeaturematrix).

* [Authorize.Net CIM](http://www.authorize.net/) - US
* [Authorize.Net](http://www.authorize.net/) - US
* [Barclays ePDQ](http://www.barclaycard.co.uk/business/accepting-payments/epdq-mpi/) - UK
* [Beanstream.com](http://www.beanstream.com/) - CA
* [BluePay](http://www.bluepay.com/) - US
* [Braintree](http://www.braintreepaymentsolutions.com) - US
* [CardStream](http://www.cardstream.com/) - GB
* [CyberSource](http://www.cybersource.com) - US
* [DataCash](http://www.datacash.com/) - GB
* [Efsnet](http://www.concordefsnet.com/) - US
* [Elavon MyVirtualMerchant](http://www.elavon.com) - US, CA
* [ePay](http://www.epay.dk/) - DK
* [eWAY](http://www.eway.com.au/) - AU
* [E-xact](http://www.e-xact.com) - CA, US
* [Federated Canada](http://www.federatedcanada.com/) - CA
* [FirstPay](http://www.first-pay.com) - US
* [Garanti Sanal POS](https://ccpos.garanti.com.tr/ccRaporlar/garanti/ccReports) - US, TR
* [Inspire](http://www.inspiregateway.com) - US
* [InstaPay](http://www.instapayllc.com) - US
* [Iridium](http://www.iridiumcorp.co.uk/) - UK, ES
* [JetPay](http://www.jetpay.com) - US
* [LinkPoint](http://www.linkpoint.com/) - US
* [Merchant e-Solutions](http://merchante-solutions.com/) - US
* [MerchantWare](http://merchantwarehouse.com/merchantware) - US
* [Modern Payments](http://www.modpay.com) - US
* [Moneris](http://www.moneris.com/) - CA
* [Netaxept](http://www.betalingsterminal.no/Netthandel-forside) - NO, DK, SE, FI
* [NetRegistry](http://www.netregistry.com.au) - AU
* [NELiX TransaX Gateway](http://www.nelixtransax.com) - US
* [NETbilling](http://www.netbilling.com) - US
* [NMI](http://nmi.com/) - US
* [Ogone DirectLink](http://www.ogone.com) - BE, DE, FR, NL, AT, CH
* [Orbital Paymentech](http://chasepaymentech.com/) - CA, US
* [PayBox Direct](http://www.paybox.com) - FR
* [PayJunction](http://www.payjunction.com/) - US
* [PaySecure](http://www.commsecure.com.au/paysecure.shtml) - AU
* [PayPal Express Checkout](https://www.paypal.com/cgi-bin/webscr?cmd=xpt/merchant/ExpressCheckoutIntro-outside) - US, CA, SG, AU
* [PayPal Payflow Pro](https://www.paypal.com/cgi-bin/webscr?cmd=_payflow-pro-overview-outside) - US, CA, SG, AU
* [PayPal Website Payments Pro (UK)](https://www.paypal.com/uk/cgi-bin/webscr?cmd=_wp-pro-overview-outside) - GB
* [PaymentExpress](http://www.paymentexpress.com/) - AU, MY, NZ, SG, ZA, GB, US
* [PayPal Website Payments Pro (CA)](https://www.paypal.com/cgi-bin/webscr?cmd=_wp-pro-overview-outside) - CA
* [PayPal Express Checkout](https://www.paypal.com/cgi-bin/webscr?cmd=xpt/merchant/ExpressCheckoutIntro-outside) - US
* [PayPal Website Payments Pro (US)](https://www.paypal.com/cgi-bin/webscr?cmd=_wp-pro-overview-outside) - US
* [Plug'n Pay](http://www.plugnpay.com/) - US
* [Protx](http://www.protx.com) - GB
* [Psigate](http://www.psigate.com/) - CA
* [PSL Payment Solutions](http://www.paymentsolutionsltd.com/) - GB
* [Quantum](http://www.quantumgateway.com) - US
* [QuickBooks Merchant Services](http://payments.intuit.com/) - US
* [Quickpay](http://quickpay.dk/) - DK, SE
* [Rabobank Nederland](http://www.rabobank.nl/) - NL
* [Realex](http://www.realexpayments.com/) - IE, GB
* [Sage Payment Solutions](http://www.sagepayments.com) - US, CA
* [Sallie Mae](http://www.salliemae.com) - US
* [SecureNet](http://www.securenet.com) - US
* [SecurePay](http://securepay.com.au) - AU
* [SecurePay](http://www.securepay.com/) - US
* [SecurePayTech](http://www.securepaytech.com/) - NZ
* [SkipJack](http://www.skipjack.com/) - US, CA
* [Stripe](https://stripe.com/welcome) - US
* [TransFirst](http://www.transfirst.com/) - US
* [TrustCommerce](http://www.trustcommerce.com/) - US
* [USA ePay](http://www.usaepay.com/) - US
* [Verifi](http://www.verifi.com/) - US
* [ViaKLIX](http://viaklix.com) - US
* [Wirecard](http://www.wirecard.com) - DE
* [WorldPay](http://www.worldpay.com) - AU, HK, GB, US

## Supported Offsite Payment Gateways

* [2 Checkout](http://www.2checkout.com)
* [Banca Sella GestPay](https://www.sella.it/banca/ecommerce/gestpay/gestpay.jsp)
* [Chronopay](http://www.chronopay.com)
* [Direct-eBanking / sofortueberweisung.de by Payment-Networks AG](https://www.payment-network.com/deb_com_en/merchantarea/home) - DE, AT, CH, BE, UK, NL
* [DirecPay](http://www.timesofmoney.com/direcpay/jsp/home.jsp)
* [HiTRUST](http://www.hitrust.com.hk/)
* [Moneybookers](http://www.moneybookers.com)
* [Nochex](http://www.nochex.com)
* [PayPal Website Payments Standard](https://www.paypal.com/cgi-bin/webscr?cmd#_wp-standard-overview-outside)
* [SagePay Form](http://www.sagepay.com/products_services/sage_pay_go/integration/form)
* [Valitor](http://www.valitor.is/) - IS
* [WorldPay](http://www.worldpay.com)

## Contributing

The source code is hosted at [GitHub](http://github.com/Shopify/active_merchant), and can be fetched using:

    git clone git://github.com/Shopify/active_merchant.git

Please see the [ActiveMerchant Guide to Contributing](http://github.com/Shopify/active_merchant/wikis/contributing) for
information on adding a new gateway to ActiveMerchant.

[![Build Status](https://secure.travis-ci.org/Shopify/active_merchant.png)](http://travis-ci.org/Shopify/active_merchant)
