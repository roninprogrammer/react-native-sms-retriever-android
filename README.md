
# reactnative-sms-retriever-api-android [![npm version](https://badge.fury.io/js/reactnative-sms-retriever-api-android.svg)](https://badge.fury.io/js/reactnative-sms-retriever-api-android)

## Getting started

`$ npm install reactnative-sms-retriever-api-android --save`

### Mostly automatic installation (RN > 0.60.0)

`$ react-native link reactnative-sms-retriever-api-android`

### Manual installation


#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.vicknesh.smsretriever.RNSmsRetrieverAndroidPackage;` to the imports at the top of the file
  - Add `new RNSmsRetrieverAndroidPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':reactnative-sms-retriever-api-android'
  	project(':reactnative-sms-retriever-api-android').projectDir = new File(rootProject.projectDir, 	'../node_modules/reactnative-sms-retriever-api-android/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      implementation project(':reactnative-sms-retriever-api-android')
  	```


## Usage
```javascript
import RNSmsRetrieverAndroid from 'reactnative-sms-retriever-api-android';

/*
 * Returns app signature array, which is used to identify the SMS sent from your server
 * callback: (optional) to receive signature array
 */
const signatureArray = await RNSmsRetrieverAndroid.getAppSignature(callback);

/*
 * Subscribe to listen for incoming SMS
 * listener: ({ message: string, error: string, code: number}) => void
 * callback: (optional) to check if subscription was successful or not
 */
const subscription = await RNSmsRetrieverAndroid.retrieveSMS(listener, callback);

// To remove subscription
subscription.remove();
```

## Note

1. App signature will vary for debug and release builds
2. Subscription will be valid for one time only. To listen for next sms, subscribe again
3. Subscription is valid for 5 minutes. After that listener will receive timeout error
4. Example SMS: "<#> Your ExampleApp code is: 123ABC78 FA+9qCX9VSu"

    **FA+9qCX9VSu** => This is your app signature
