# react-native-upi-payment

<img width="778" alt="art" src="https://user-images.githubusercontent.com/13037986/46161228-a1369700-c2a2-11e8-9b9d-d0c40a3e0f38.png">

[react-native-upi](https://www.npmjs.com/package/react-native-upi-payment) is a tiny plugin to integrate the UPI payment interface made by [NPCI](https://www.bhimupi.org.in/) from your react native apps. This plugin allows you to enable peer to peer payments via UPI in your react native apps. Linking specs have been followed as per [this](https://www.npci.org.in/sites/all/themes/npcl/images/PDF/UPI_Linking_Specs_ver_1.5.1.pdf) doc

## Installation

```bash
npm install react-native-upi-payment
```

or

```bash
yarn add react-native-upi-payment
```

### Android

#### Automatic Installation

```
react-native run link
```

#### Manual Installation

Open `android/settings.gradle` add the following

```
include ':react-native-upi-payment'
project(':react-native-upi-payment').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-upi-payment/android')

```

Open `android/build.gradle` add the following in the dependencies section

```
dependencies {
    compile project(':react-native-upi-payment')
}
```

Open `MainApplication.java`

```java
// Other imports
import com.upi.payment.UpiPaymentPackage;

  // Add this in the Main Application Class
  @Override
  protected List<ReactPackage> getPackages() {
    return Arrays.<ReactPackage>asList(
       //... Other packages
          new UpiPaymentPackage() // <- Add this line
    );
  }
```

## Usage

```javascript
RNUpiPayment.initializePayment(
  {
    vpa: "john@upi", // or can be john@ybl or mobileNo@upi
    payeeName: "John Doe",
    amount: "1",
    transactionRef: "aasf-332-aoei-fn",
  },
  successCallback,
  failureCallback
);
```

## Config docs

```javascript
{
  /*
  * REQUIRED
  * All felids
  */
  vpa: 'vap@app',
  payeeName: 'Mohit Mawar',
  transactionId:'any time uniqe'
  transactionRef:'any time uniqe',
  amount: '10',
  transactionNote: 'for food'
  merchantCode: '0000',
  mode:'02',
  purpose:'00'
}
```

## Callbacks

```javascript
function successCallback(data) {
  // do whatever with the data
}

function failureCallback(data) {
  // do whatever with the data
}
```

## Responses

SUCCESS CASE

```javascript
{
/**
* SUCCESS STATUS
* */
Status: "SUCCESS",
/**
* Transaction Id of bank to which upi has been initiated
* */
txnId: "AXId8c71205eb7d459889bb7018bdf2c056",
/**
* 00 response code, for success
* transaction is successful money has been debited
* */
responseCode: "00",
/**
* Transaction reference stated in init obect
* */
txnRef: "aasf-332-aoeifn"

}
```

FAILURE CASES

```javascript
{
  /**
   * Status Sent on transaction
   * If the user presses back or closes app
   * */
  status: "FAILURE",

  /**
  * If the user presses back or closes app
  * */
  message: "No action taken"
} // No action
```

```javascript
{
  /**
  * FAILURE STATUS
  * */
  Status: "FAILURE",
  /**
  * Transaction Id of bank to which upi has been initiated
  * */
  txnId: "AXIa463c7ca81a24e168df5ac9c1359c38c",
  /**
  * Non 0 response code,
  * If the user enters the wrong pin
  * */
  responseCode: "ZM",
  /**
  * Transaction reference stated in init obect
  * */
  txnRef: "aasf-332-aoeifn"

  }
```
