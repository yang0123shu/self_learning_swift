# Counter App - SwiftUI Example Project

## Project Overview
A simple counter app that demonstrates basic SwiftUI concepts including state management, buttons, and text formatting.

## What You'll Learn
- @State property wrapper
- Button actions
- Text formatting
- VStack layout
- Basic styling with modifiers

## Complete Code

```swift
import SwiftUI

struct CounterApp: View {
    @State private var count = 0
    
    var body: some View {
        VStack(spacing: 30) {
            // Title
            Text("Counter App")
                .font(.largeTitle)
                .bold()
            
            // Counter display
            Text("\(count)")
                .font(.system(size: 80, weight: .bold))
                .foregroundColor(count < 0 ? .red : count > 0 ? .green : .blue)
                .padding()
                .background(Color.gray.opacity(0.1))
                .cornerRadius(20)
            
            // Buttons
            HStack(spacing: 20) {
                Button(action: {
                    count -= 1
                }) {
                    Image(systemName: "minus.circle.fill")
                        .font(.system(size: 50))
                        .foregroundColor(.red)
                }
                
                Button(action: {
                    count = 0
                }) {
                    Image(systemName: "arrow.clockwise.circle.fill")
                        .font(.system(size: 50))
                        .foregroundColor(.gray)
                }
                
                Button(action: {
                    count += 1
                }) {
                    Image(systemName: "plus.circle.fill")
                        .font(.system(size: 50))
                        .foregroundColor(.green)
                }
            }
            
            // Statistics
            VStack(spacing: 10) {
                Text("Statistics")
                    .font(.headline)
                
                HStack {
                    VStack {
                        Text("Status")
                            .font(.caption)
                            .foregroundColor(.gray)
                        Text(count == 0 ? "Zero" : count > 0 ? "Positive" : "Negative")
                            .font(.subheadline)
                            .bold()
                    }
                    .frame(maxWidth: .infinity)
                    
                    Divider()
                        .frame(height: 40)
                    
                    VStack {
                        Text("Absolute")
                            .font(.caption)
                            .foregroundColor(.gray)
                        Text("\(abs(count))")
                            .font(.subheadline)
                            .bold()
                    }
                    .frame(maxWidth: .infinity)
                }
                .padding()
                .background(Color.gray.opacity(0.1))
                .cornerRadius(10)
            }
            .padding(.horizontal)
        }
        .padding()
    }
}

// Preview
struct CounterApp_Previews: PreviewProvider {
    static var previews: some View {
        CounterApp()
    }
}
```

## How to Use

1. Create a new SwiftUI project in Xcode
2. Replace the content of `ContentView.swift` with the code above
3. Run the app in the simulator or preview

## Features

- **Increment**: Tap the green plus button to increase the counter
- **Decrement**: Tap the red minus button to decrease the counter
- **Reset**: Tap the gray reset button to set the counter back to zero
- **Color Coding**: The counter changes color based on its value
  - Blue: Zero
  - Green: Positive numbers
  - Red: Negative numbers
- **Statistics**: Shows the status and absolute value of the counter

## Exercises to Extend This App

1. **Add Step Control**: Add buttons to increment/decrement by 5 or 10
2. **Add History**: Keep track of all values and show them in a list
3. **Add Limits**: Set maximum and minimum values the counter can reach
4. **Add Sound**: Play a sound effect when incrementing or decrementing
5. **Add Animation**: Animate the number changes
6. **Save State**: Persist the counter value using UserDefaults
7. **Multiple Counters**: Create multiple independent counters

## Concepts Used

### @State
```swift
@State private var count = 0
```
The `@State` property wrapper allows SwiftUI to track changes and update the UI automatically.

### Conditional Styling
```swift
.foregroundColor(count < 0 ? .red : count > 0 ? .green : .blue)
```
Changes the text color based on the counter value.

### Layout with VStack and HStack
```swift
VStack(spacing: 30) {
    // Vertical arrangement
    HStack(spacing: 20) {
        // Horizontal arrangement
    }
}
```

### Button Actions
```swift
Button(action: {
    count += 1
}) {
    // Button appearance
}
```

## Next Steps
After mastering this app, try building:
- A tip calculator
- A unit converter
- A simple calculator
- A BMI calculator
