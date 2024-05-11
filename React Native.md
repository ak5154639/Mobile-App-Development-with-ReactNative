# React Native
  - A framework that relies on React core
  - Allows us to build mobile apps using only JavaScript
    - "Learn once, write anywhere"
  - Supports iOS and Android

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
      <video autoplay loop muted width="500">
        <source src="https://raw.githubusercontent.com/ak5154639/Mobile-App-Development-with-ReactNative/main/assets/blockJSDemo.mp4" type="video/mp4">
        Your browser does not support the video tag.
      </video>



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
