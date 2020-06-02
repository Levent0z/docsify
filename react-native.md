# React Native: Getting Started

## Documentation
[Getting Started (Official)](https://facebook.github.io/react-native/docs/gettings-started.html)

## Setup
```bash
npm i -g create-react-native-app
create-react-native-app _name_
cd _name_
yarn start
```

Install `Expo` app from the Play Store on Android or App Store on iPhone.

Use email links to connect Expo to the React Native app.

> Shake the phone to show the Expo dev tools menu.

> If you're bundle gets stuck downloading at 100%, simply restart it via the Expo dev-tools menu.

### Ignoring Warnings

```JavaScript
import { YellowBox } from 'react-native';
YellowBox.ignoreWarnings{[
    'Warning: componentWillMoint is deprecated',
    'Warning: componentWillReceiveProps is deprecated',
]};
``` 



## Custom Component (Class Style)

```JavaScript
import React, { Component } from 'react';
import { StyleSheet, Text, View } from 'react-native';
import PropTypes from 'prop-types';

export default class MyComponent extends Component {
    state = {
    };

    componentDidMount() {
        //...
    }
    render() {
        // return JSX
    }
}
```

## Custom Component (Functional Style) with props and styles
```JavaScript
import { View, StyleSheet } from 'react-native';
import PropTypes from 'prop-types';

const styles = StyleSheet.create({
    someStyleProperty: 'dependsOnTheProperty'
});

export default function MyOtherComponent({ someObject }) {
    return (
        <Views style={styles.someStyleProperty}/>
    );
}

MyOtherComponent.propTypes = {
    someObject: PropTypes.shape({
        someStringProperty: PropTypes.string.isRequired,
        someDateProperty: PropTypes.instanceOf(Date)
    }),
};
```

## Navigation


```JavaScript
import { StackNavigator } from 'react-navigation';
import MyComponent1 from './MyComponent1';
import MyComponent2 from './MyComponent2';

export default StackNavigator({
    navKey1: {
        screen: MyComponent1,
        navigationOptions: () => ({
            title: 'My Title 1'
        })
    },
    navKey2: {
        screen: MyComponent2,
        navigationOptions: () => ({
            title: 'My Title 2'
        })
    }
});
```
> Any component that gets displayed in the navigator gets a `navigation` prop. Use it to navigate as follows:
> 
> ```JavaScript
> this.props.navigation.navigate('navKey2'); // or 'navKey1'
> ```
> To go back, simply:
> ```JavaScript
> this.props.navigation.goBack();   
> ```


## Useful Tips

### Interesting Imports:
```JavaScript
import { TouchableHighlight } from 'react-native'; // Makes its content touchable
import DateTimePicker from 'react-native-modal-datetime-picker'; // Separate NPM package
```

### Making HTTP requests

Use the promise based `fetch` api.

### Quick JSON-file-based REST server
Use [JSON Server](https://github.com/typicode/json-server) to watch and serve a static JSON file. Supports GET and POST. 
To install and use:
```sh
yarn global add json-server
json-server someFile.json
```

### Accessing the local computer from the app running on Expo
```JavaScript
import Export from 'expo';
const { manifest } = Expo.Constants;
const api = maniest.packagerOpts.dev ? manifest.debuggerHost.split(':').shift().concat(':3000') : 'production_url_here';
const url = `http://${api}/`;
```

### Getting rid of Expo (i.e. `eject`ing your app)
```sh
yarn run eject
```