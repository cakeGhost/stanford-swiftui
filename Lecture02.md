## struct으로 코드 중복 없애기

```swift
struct ContentView02: View {
    var body: some View {
        HStack {
            CardView()
            CardView()
            CardView()
            CardView()
        }
        .padding(.horizontal)
        .foregroundColor(.red)
        
    }
}

struct CardView: View {
    var body: some View {
        ZStack {
            RoundedRectangle(cornerRadius: 20)
                .stroke(lineWidth: 3)
            Text("😈")
                .font(.largeTitle)
        }
    }
}
```
![image](https://user-images.githubusercontent.com/94977962/147564784-115e9943-9a32-4d57-9dc1-1d1bfe1999d2.png)

<br>
<br>


# 다크모드
```
struct ContentView02_Previews: PreviewProvider {
    static var previews: some View {
        ContentView02()
            .preferredColorScheme(.dark)
        ContentView02()
            .preferredColorScheme(.light)
    }
}
```

![image](https://user-images.githubusercontent.com/94977962/147564767-7ab91660-a13c-4995-8dbf-593e496f4f5b.png)



<br>
<br>

# @State 

![image](https://user-images.githubusercontent.com/94977962/147564978-fd747ee2-e3bf-4aae-8a09-d8f0a497eaa0.png)

state값이 변경되면 view가 appearance를 invalidates하고 body를 다시 계산함 

(UIKit에선 Property Observer를 통해서 변화가 일어나면 View를 업데이트시키는방식으로 함)

SwiftUI에선 `@State`라는 Property wrapper를 통해서 같은 일을 함.


![image](https://user-images.githubusercontent.com/94977962/147564859-24a4229f-9c81-4fab-9a6e-90c3ba8d0a48.png)

```
struct ContentView02: View {
    var body: some View {
        HStack {
            CardView()
            CardView()
            CardView()
            CardView()
        }
        .padding(.horizontal)
        .foregroundColor(.red)
        
    }
}

struct CardView: View {
    @State var isFaceUp: Bool = true
    
    var body: some View {
        ZStack {
            let shape: RoundedRectangle = RoundedRectangle(cornerRadius: 20)
            
            if isFaceUp {
                shape.fill().foregroundColor(.white)
                shape.stroke(lineWidth: 3)
                Text("😈").font(.largeTitle)
            } else {
                shape.fill()
            }
            
        }
        .onTapGesture {
            isFaceUp = !isFaceUp
        }
    }
}
```

ZStack의 결과를 onTapGesture의 결과로  isFaceUp을 변경할 때 실제로 메모리 어딘가에서 변경함

(`@State` property wrapper를 사용하여, SwiftUI가 해당 메모리를 관리하도록 함)


<br>
<br>


