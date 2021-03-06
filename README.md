***WARNING***: This library is a work in progress

# React Native Watch Connectivity

Communicate with your apple watch apps over the react native bridge.

**Note:** This library does not allow you to write your iWatch apps in React Native but rather allows your RN iOS app to communicate with a watch app written in Obj-C/Swift.

<img height=600 src="https://raw.githubusercontent.com/mtford90/react-native-watch-connectivity/master/assets/screenshot.png"/>

## Demo

The featured screenshot is from the demo app. To get the demo app going:

```
git clone https://github.com/mtford90/react-native-watch-connectivity.git
cd react-native-watch-connectivity
npm install
cd ios
pod install
open buff.xcworkspace
```

And then run the app!

## Install

```bash
npm install react-native-watch-connectivity
```

Then add `node_modules/react-native-watch-connectivity/RNWatch.xcodeproj` to your project and ensure that libRNWatch.a is present in the **Link Binary With Libraries** build phase

## Usage

**ES6**

```js
import * as watch from 'react-native-watch-connectivity'
```

**ES5**

```js
var watch = require('react-native-watch-connectivity')
```

### Reachability

```js
// Monitor reachability
const unsubscribe = watch.subscribeToWatchReachability(watchIsReachable => {
    this.setState({watchIsReachable})
})

// Get current reachability
watch.getReachability(watchIsReachable => {
  // ...
})
```

### Watch State

```js
// Monitor watch state
const unsubscribe = watch.subscribeToWatchState(watchState => {
    console.log('watchState', watchState) // NotActivated, Inactive, Activated
})

// Get current watch state
watch.getWatchState(watchState => {
    console.log('watchState', watchState) // NotActivated, Inactive, Activated
})
```

### Messages

#### Send Message

Send messages and receive replies

```js
watch.sendMessage({text: "Hi watch!"}, (err, replyMessage) => {
    console.log("Received reply from watch", replyMessage)
})
```

#### Receive Message

Recieve messages and send responses

```js
const unsubscribe = watch.subscribeToMessages((err, message, reply) => {
    if (!err) reply({text: "message received!"})
})
```

### Message Data

TODO: Undocumented & partially implemented

### Files

#### Send Files

```js
const uri = 'file://...' // e.g. a photo/video obtained using react-native-image-picker

watch.transferFile(uri).then(() => {
  // ...
}).catch(err => {
  // ... handle error
})
```

#### Receive Files

TODO: Not implemented or documented

### User Info

```
const unsubscribe = watch.subscribeToUserInfo((err, info) => {
    // ...
})
```

```
watch.sendUserInfo({name: 'Mike', id: 5})
```

```
watch.getUserInfo().then(info => {
    // ...
}).catch(err => {
    // ...
})
```

###

