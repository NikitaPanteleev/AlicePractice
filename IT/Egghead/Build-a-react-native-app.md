https://egghead.io/courses/build-a-react-native-application-for-ios-and-android-from-start-to-finish

And idea to try:
https://egghead.io/lessons/react-course-introduction-progressive-web-apps-in-react-with-create-react-app

Saga:
https://egghead.io/courses/async-react-with-redux-saga
And components:
https://codecanyon.net/item/antiqueruby-react-native/21331228?s_rank=3&_ga=2.50842665.1642134547.1554493962-115958582.1554493962


For redux:
https://egghead.io/lessons/redux-introduction-to-using-the-state-adt-with-redux

React navigation:
https://egghead.io/courses/react-navigation-for-native-mobile-applications

# Boilerplate setup
https://www.npmjs.com/package/ignite-boilerplate-andross-typescript#usage
```
ignite new journal -b ignite-boilerplate-andross-typescript
ignite g container Journal
```
Then open ios project in Xcode and add Javascript core dependency.

## React native api
`<Text>` - text component. 

## Views
### <TextInput>
```
state = {
  search: null
}

<TextInput 
  style={styles.input} 
  placeholder="Live Search"
  onChangeText={text => {
            this.setState({ search: text })
  }}
  value={this.state.search}
/>
```
### <ScrollView>
To Fix padding:
```
<ScrollView contentContainerStyle={{
  paddingTop: 30
}}>
```
For hunders/thousands use `<FlatList>`
### <FlatList>
```
<FlatList
  data = {dataList}
  renderItem={({ item, index }) => 
    <RestaurantRow place={item} index={index} />
  }
  keyExtractor={item => item.name}
  initialNumToRender={16}
/>
```
### Touchable
For buttons:  `TouchableOpacity, TouchableHighlight, TouchableWithoutFeedback`

### Image
```
<Image 
      source={{ 
        uri: `http://localhost:3000/images/${place.image}`
      }}
      srtyle={{
          flex:1,
          height:100
      }}
      resizeMode="contain"
    />
```

### Vector graphics
```
npm install --save react-native-vector-icons
react-native link
```
https://fontawesome.com/icons?d=gallery
```
import Icon from 'react-native-vector-icons/FontAwesome'
```

### React-navigation
### keyboard-aware-scroll-view
`npm install react-native-keyboard-aware-scroll-view`

### Splash screen
```
npm install --save react-native-splash-screen
react-native link
```
Then add to `AppDelegate.m` 


## Flex
```
style={{
        flex: 1
      }}
```
Default direction is column. For rows specify `flexDirection: 'row'`


## Debugging
### console log
`cmd + D` on iOs simulator

### debugger
Just put `debugger` into source code.
### style for custom platform.
Files ending on `.ios.js` and `.android.js`

## axios to fetch http
```
axios.get('http://localhost:3000/restaurants')
    .then(result => this.setState({ restaurants: result.data }))
```

## stack navigation
```
npm install --save react-navigation
```