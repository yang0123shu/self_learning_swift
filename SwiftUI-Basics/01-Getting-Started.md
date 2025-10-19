# Getting Started with SwiftUI

## Introduction
SwiftUI is Apple's modern framework for building user interfaces across all Apple platforms. It uses a declarative syntax that's easy to read and write.

## What is SwiftUI?
- **Declarative**: You describe what you want, not how to build it
- **Cross-platform**: Works on iOS, macOS, watchOS, and tvOS
- **Live Preview**: See changes instantly in Xcode
- **Native**: Built on top of native UIKit/AppKit components

## Your First SwiftUI View

### Basic View
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, SwiftUI!")
    }
}

// Preview
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

### Understanding the Structure
1. `import SwiftUI` - Imports the SwiftUI framework
2. `struct ContentView: View` - Defines a view that conforms to the View protocol
3. `var body: some View` - Required property that describes the view's content
4. `ContentView_Previews` - Enables live preview in Xcode canvas

## Basic SwiftUI Views

### Text
Display text with various styles:

```swift
struct TextExamples: View {
    var body: some View {
        VStack(spacing: 20) {
            Text("Simple Text")
            
            Text("Bold Text")
                .bold()
            
            Text("Large Title")
                .font(.largeTitle)
            
            Text("Red Text")
                .foregroundColor(.red)
            
            Text("Multiline text that wraps to multiple lines when it's too long for one line")
                .multilineTextAlignment(.center)
                .lineLimit(3)
        }
        .padding()
    }
}
```

### Image
Display images:

```swift
struct ImageExamples: View {
    var body: some View {
        VStack(spacing: 20) {
            // System icon
            Image(systemName: "star.fill")
                .font(.largeTitle)
                .foregroundColor(.yellow)
            
            // Custom image (from Assets)
            Image("myImage")
                .resizable()
                .scaledToFit()
                .frame(width: 200, height: 200)
                .cornerRadius(10)
        }
    }
}
```

### Button
Interactive buttons:

```swift
struct ButtonExamples: View {
    @State private var counter = 0
    
    var body: some View {
        VStack(spacing: 20) {
            Text("Counter: \(counter)")
                .font(.title)
            
            Button("Increment") {
                counter += 1
            }
            
            Button(action: {
                counter -= 1
            }) {
                Text("Decrement")
                    .padding()
                    .background(Color.red)
                    .foregroundColor(.white)
                    .cornerRadius(8)
            }
        }
    }
}
```

## Layout Containers

### VStack - Vertical Stack
```swift
struct VStackExample: View {
    var body: some View {
        VStack(spacing: 15) {
            Text("First")
            Text("Second")
            Text("Third")
        }
    }
}
```

### HStack - Horizontal Stack
```swift
struct HStackExample: View {
    var body: some View {
        HStack(spacing: 15) {
            Text("Left")
            Text("Center")
            Text("Right")
        }
    }
}
```

### ZStack - Depth Stack
```swift
struct ZStackExample: View {
    var body: some View {
        ZStack {
            Rectangle()
                .fill(Color.blue)
                .frame(width: 200, height: 200)
            
            Text("On Top")
                .foregroundColor(.white)
                .font(.title)
        }
    }
}
```

## Modifiers
Modifiers change the appearance and behavior of views:

```swift
struct ModifierExamples: View {
    var body: some View {
        VStack {
            Text("Styled Text")
                .font(.title)
                .foregroundColor(.blue)
                .padding()
                .background(Color.yellow)
                .cornerRadius(10)
                .shadow(radius: 5)
            
            Image(systemName: "heart.fill")
                .font(.system(size: 50))
                .foregroundColor(.red)
                .padding()
                .background(Color.white)
                .clipShape(Circle())
                .shadow(color: .gray, radius: 10, x: 0, y: 5)
        }
    }
}
```

## State Management

### @State
For simple, view-local state:

```swift
struct StateExample: View {
    @State private var isOn = false
    
    var body: some View {
        VStack {
            Toggle("Switch", isOn: $isOn)
                .padding()
            
            Text(isOn ? "ON" : "OFF")
                .font(.title)
                .foregroundColor(isOn ? .green : .red)
        }
    }
}
```

### @Binding
Share state between views:

```swift
struct ParentView: View {
    @State private var text = ""
    
    var body: some View {
        VStack {
            ChildView(text: $text)
            Text("You entered: \(text)")
        }
    }
}

struct ChildView: View {
    @Binding var text: String
    
    var body: some View {
        TextField("Enter text", text: $text)
            .textFieldStyle(RoundedBorderTextFieldStyle())
            .padding()
    }
}
```

## Common UI Elements

### TextField
```swift
struct TextFieldExample: View {
    @State private var name = ""
    @State private var email = ""
    
    var body: some View {
        VStack(spacing: 20) {
            TextField("Name", text: $name)
                .textFieldStyle(RoundedBorderTextFieldStyle())
            
            TextField("Email", text: $email)
                .textFieldStyle(RoundedBorderTextFieldStyle())
                .autocapitalization(.none)
                .keyboardType(.emailAddress)
            
            Text("Name: \(name)")
            Text("Email: \(email)")
        }
        .padding()
    }
}
```

### Toggle
```swift
struct ToggleExample: View {
    @State private var isEnabled = false
    @State private var notifications = true
    
    var body: some View {
        VStack(alignment: .leading, spacing: 20) {
            Toggle("Enable Feature", isOn: $isEnabled)
            Toggle("Notifications", isOn: $notifications)
        }
        .padding()
    }
}
```

### Slider
```swift
struct SliderExample: View {
    @State private var value = 50.0
    
    var body: some View {
        VStack {
            Text("Value: \(Int(value))")
                .font(.title)
            
            Slider(value: $value, in: 0...100, step: 1)
                .padding()
        }
    }
}
```

## Practical Example: Complete View

```swift
struct WelcomeView: View {
    @State private var name = ""
    @State private var showGreeting = false
    
    var body: some View {
        VStack(spacing: 30) {
            Text("Welcome!")
                .font(.largeTitle)
                .bold()
            
            Image(systemName: "person.circle.fill")
                .font(.system(size: 100))
                .foregroundColor(.blue)
            
            TextField("Enter your name", text: $name)
                .textFieldStyle(RoundedBorderTextFieldStyle())
                .padding(.horizontal)
            
            Button(action: {
                showGreeting = true
            }) {
                Text("Submit")
                    .font(.headline)
                    .foregroundColor(.white)
                    .padding()
                    .frame(maxWidth: .infinity)
                    .background(Color.blue)
                    .cornerRadius(10)
            }
            .padding(.horizontal)
            .disabled(name.isEmpty)
            
            if showGreeting {
                Text("Hello, \(name)!")
                    .font(.title2)
                    .foregroundColor(.green)
            }
        }
        .padding()
    }
}
```

## Next Steps
1. Practice building simple views
2. Experiment with different modifiers
3. Combine multiple views
4. Learn about navigation and lists
5. Explore animations and transitions

## Resources
- Apple's SwiftUI Documentation
- SwiftUI Tutorials on Apple Developer
- Hacking with Swift - 100 Days of SwiftUI
- Paul Hudson's SwiftUI by Example
