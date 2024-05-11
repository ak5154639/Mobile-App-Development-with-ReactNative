# React Native
  - A framework that relies on React core
  - Allows us to build mobile apps using only JavaScript
    - "Learn once, write anywhere"
  - Supports iOS and Android

## Setting up Development Environment
  - Download Android `Node.js`, `jdk` and `npm` latest versions or simply install using `choco`:
    ```
      choco install -y nodejs-lts microsoft-openjdk17
    ```
  - Then download Andorid Studio this will setup everything for you otherwise it is very complex to configure manually you can read react native decumentaion.
  - Start `react-native` app by writting below command:
    ```
      npx react-native@latest init AwesomeProject
    ```
  - Run application using
  1. Target is Android Device:
    ```
      npx react-native run-android
    ```
  2. Target is iOS:
    ```
      npx react-native run-ios
    ```
  - If you are getting error and you app didn't run yet just run command below it will check errors and after thet pressing `f` will automatically try to fix error
    ```
      npx react-native run-android
    ```
## How does React Native work?
  - JavaScript is bundled
    - Transpiled and minified
  - Separate threads for UI, layout and JavaScript
  - Communicate asynchronously through a "bridge"
    - JS thred will request UI elements to be shown
    - JS thread can be blocked and UI will still work
      ![image](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative/assets/60311459/42ae2269-afe4-48d8-b161-a0f9d1f8a02a) <br/>
      Below is code for the demonstration that React Native Apps handdle UI and JS through separate threads and communicate with each other through bridge
      ```
        export default class App extends Component {
            blockJS(){
                const done = Date.now() + 5000;
                console.log("Blocking!");
                let i = 5
                while(Date.now() < done){
                    if(Date.now() == done - i){
                        console.log(Date.now());
                    }
                    i=i-1;
                }
                console.log("Unblocking!");
            }
            render(){
                return (
                    <View style={styles.container}>
                      <ScrollView contentContainerStyle={styles.contentContainer}>
                        <View style={styles.content}>
                          <Text style={styles.text}>Content 1</Text>
                        </View> 
                        {/* Multiple times to make container overflow so can be scrollable */}
                        <View style={styles.content}>
                            <Button title="block JS" style={styles.content} onPress={()=>this.blockJS()} />
                        </View>        
                        <View style={styles.content}>
                          <Text style={styles.text}>Content 8</Text>
                        </View>
                      </ScrollView>
                    </View>
                );
            }
        }
      ```
      ![blockJSDemo](https://github.com/ak5154639/Mobile-App-Development-with-ReactNative/assets/60311459/42e22a21-ed8b-4880-9756-74a15905fb13) <br/>
      In above screen recording we can see that I clicked `bolck JS` button and my JS was blocked for that time but my UI was still responsive.




## Differences between React Native and Web
  - Base components
  - Style
  - No browser APIs
    - CSS animations, Canvas, SVG, etc.
    - Some have been polyfilled (fetch, timers, console, etc.)
  - Navigation

## React Native Components
  - Not globally in scope like React web components
    - Import from 'react-native'
  - div -> View
  - span -> Text
    - All text must be wrapped by a <Text /> tag
  - button -> Button
  - ScrollView
    [see documentation for more compenents and APIs](https://facebook.github.io/react-native/docs/components-and-apis.html)

## Style
  - React Native uses JS objects for styling
  - Object keys are based on CSS properties
  - Flexbox layout
    - Default to column layout
  - Lengths are in unitless numbers
  - `style` prop can take an array of styles
  - `StyleSheet.create()`
    - Functionally the same as creating objects for style
    - Additional optimization: only send IDs over the bridge
