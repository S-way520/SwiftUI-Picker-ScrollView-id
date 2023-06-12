# SwiftUI-Picker-ScrollView-id
For details, please refer to the picture.
# The first part
![IMG_0091](https://github.com/S-way520/SwiftUI-Picker-ScrollView-id/assets/95877651/17a02805-b91b-4155-bf64-88b5fdaf5b86)
# The scond part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
struct ContentView: View {
    @State private var selectedRect = 0
    var body: some View {
        VStack {
            Picker("Select rect", selection: $selectedRect) {
                ForEach(0..<4, id: \.self) { index in
                    Text("Rect \(index)")
                }
            }
            .pickerStyle(MenuPickerStyle())
            ScrollViewReader { scrollViewProxy in
                ScrollView(.horizontal, showsIndicators: false) {
                    LazyHStack(spacing: 10) {
                        ForEach(0..<4, id: \.self) { index in
                            Rectangle()
                                .fill(Color.blue)
                                .frame(width: 200, height: 200)
                                .id(index)
                        }
                    }
                }
                .onChange(of: selectedRect) { rectIndex in
                    scrollViewProxy.scrollTo(rectIndex, anchor: .center)
                }
            }
            .frame(height: 200)
        }
    }
}
```
