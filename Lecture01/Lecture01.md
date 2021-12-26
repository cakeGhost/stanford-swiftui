#View
View는 프로토콜 구조로 되어있음 

View 프로토콜을 채택, 준수한 타입을 통해서 커스텀 뷰를 생성할 수 있음 

```
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("hello world")
            .padding()
    }
}

struct ContentView_Preivews: PreviewProvider {
    static var previews: some View {
       ContentView()
    }
}
```

`var body: some View` 는

`var i: Int` 처럼 반환타입이 View인 것임


```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .padding()
    }
}
```

<br>
<br>

# Functional Programming

```swift
struct ContentView: View {
    var body: Text {
        return Text("Hello, world!")    
    }
}
```

# Padding

```swift
var body: some View {
        return Text("Hello, world!")
            .padding(.all)
}
```


.padding() 이건 default 패딩값! 기본값 쓰는 경우가 많다고함...! _ ! 

body를 Text로 변경하면 에러남! 

View.padding이 아니기 때문,, 


Text의 속성을 추가할 때마다 추가됨.. 

```swift
var body: some View {
        return Text("Hello, world!")
            .foregroundColor(Color.purple)
            .padding()
    }
```

<br>
<br>

# .stroke()
```
   return RoundedRectangle(cornerRadius: 25.0).stroke().padding(.horizontal)
```

<img width="290" alt="stroke" src="https://user-images.githubusercontent.com/94977962/147403357-d161dbee-fc3f-4427-9e14-732f12f24cc5.png">


```swift
.stroke(line

: 3)
```


<br>
<br>


# ZStack

<img width="500" alt="Zstack" src="https://user-images.githubusercontent.com/94977962/147403370-4a37814f-0bb8-4802-9ca8-aaef398d44e5.png">

ZStack은 Stack안에 있는 자식 뷰들을 z축으로 중첩시켜주는 view

```swift
import Foundation
import SwiftUI

struct ContentView02: View {
    var body: some View {
        
        return ZStack(content: {
            RoundedRectangle(cornerRadius: 25.0)
                .stroke(lineWidth: 3)
                .padding(.horizontal)
                .foregroundColor(.yellow)
            
            Text("Hello Betty")
                .foregroundColor(.pink)
                .padding()
        })
        
    }
}

struct ContentView02_Previews: PreviewProvider {
    static var previews: some View {
        ContentView02()
            
    }
}
```

ZStack의 속성이 

ZStack안에 들어있는 자식들한테 적용이 됨 

<img width="292" alt="ex01" src="https://user-images.githubusercontent.com/94977962/147403385-306074a6-b75a-4964-8dcb-cdd40cd39023.png">


즉, 위에거랑 아래거랑 똑같은거임~! 

<img width="293" alt="ex02" src="https://user-images.githubusercontent.com/94977962/147403387-e8877a3c-a053-473e-9a90-c780fac45065.png">


기본값 주고 싶을때 사용

완성 🎉

```
Zstack {
    RoundedRectangle(cornerRadius: 25.0)
        .stroke(lineWidth: 3)
    Text("Hello cake")
        .foregroundColor(.black)
}
.padding(.horizontal)
.foregroundColor(.red)
}
```
