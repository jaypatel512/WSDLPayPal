# WSDLPayPal

- Run `mvn clean package -Dmaven.javadoc.skip=true`, to convert wsdl to jar.
- Use that jar to create a request.

- This are our observations:

```java
package com.jay.sample;

import com.example.PayPalAPIInterfaceServiceStub.AirlineItineraryType;
import com.example.PayPalAPIInterfaceServiceStub.DoExpressCheckoutPaymentRequestDetailsType;
import com.example.PayPalAPIInterfaceServiceStub.EnhancedDataType;
import com.example.PayPalAPIInterfaceServiceStub.EnhancedPaymentDataType;
import com.example.PayPalAPIInterfaceServiceStub.PaymentDetailsType;

public class Main {

	public static void main(String[] args) {
		
		// Created a simple airline itinerary data
		AirlineItineraryType airlineItinerary = new AirlineItineraryType();
		airlineItinerary.setTicketNumber("123");
		
		EnhancedPaymentDataType enhancedPaymentData = new EnhancedPaymentDataType();
		//enhancedPaymentData.setAirlineItinerary() DOES NOT EXIST.
		
		EnhancedDataType enhancedDataType = new EnhancedDataType();
		enhancedDataType.setAirlineItinerary(airlineItinerary); // EXISTS.
		
		// Trying to add the enhanced Data to paymentDetails
		PaymentDetailsType paymentDetails = new PaymentDetailsType();
		paymentDetails.setEnhancedPaymentData(enhancedPaymentData);
		//paymentDetails.setEnhancedData(); DOES NOT EXIST.
		
		DoExpressCheckoutPaymentRequestDetailsType request = new DoExpressCheckoutPaymentRequestDetailsType();
		request.setEnhancedData(enhancedDataType);
		request.addPaymentDetails(paymentDetails);
	}
}

```
