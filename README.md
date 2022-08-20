# HelloAppleWatch
![image](https://user-images.githubusercontent.com/47273077/185726085-22a4f669-a3eb-40ae-86b1-007c0b4b43e2.png)

## Hello Apple Watch
<img width="378" src="https://user-images.githubusercontent.com/47273077/185726120-b04ebd20-3bb6-4aba-98c7-222d274ed602.gif">

ContentView
```swift
struct ContentView: View {
    
    @StateObject private var sentence = EmojiSentence()
    
    var body: some View {
        VStack {
            Image("Cookie")
                .resizable()
                .scaledToFit()
                .overlay(
                    Text(sentence.emoji)
                        .font(.title3)
                        .padding(.top, 10)
                        .buttonStyle(.plain)
                )
            Text(sentence.text)
                .font(.caption)
                .padding(.top, 20)
        }
        .onTapGesture {
            sentence.next()
        }
    }
}

```

EmojiSentence
```swift
@MainActor
class EmojiSentence: ObservableObject {
    @Published var text = ""
    @Published var emoji = ""

    private let sentences = [
        (text: "Not my cup of tea", emoji: "🙅‍♀️ ☕️"),
        (text: "Talk to the hand", emoji: "🎙 ✋"),
        (text: "Not the brightest bulb", emoji: "🚫 😎 💡"),
        (text: "When pigs fly", emoji: "⏰ 🐷 ✈️"),
        (text: "Boy who cried wolf", emoji: "🚶😭🐺")
    ]
    private var index = 0

    init() {
        update()
    }

    func next() {
        index += 1
        if index == sentences.count {
            index = 0
        }

        update()
    }

    private func update() {
        text = sentences[index].text
        emoji = sentences[index].emoji
    }
}
```
