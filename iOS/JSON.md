# JSON

> 주요 내용: JSON, Parsing의 개념, codable 프로토콜, 

## JSON 이란

- **J**ava**S**cript **O**bject **N**otation

- "**네트워크를 통해 데이터를 주고받는 데 자주 사용되는 경량의** **데이터 형식**"

- JSON은  name - value 형태의 쌍으로 이루어져 있음

## Parsing 이란

> 컴퓨터 과학에서 파싱((syntactic) parsing)은 일련의 문자열을 의미있는 토큰(token)으로 분해하고 이들로 이루어진 파스 트리(parse tree)를 만드는 과정을 말한다.

-  JSON, XML, HTML 등으로 구성된 데이터를 분석하여 원하는 부분만 추출하고자 하는 것을 의미함

- 참고)
  https://www.scienceall.com/파싱parsing/

   

## [Swift]

##  `codable`을 이용해서 JSON Parsing하기

 iOS 에서는 `swift` 의 인스턴스를 `JSON` 형식으로 변환하거나 반대로 가져올 때 인코딩과 디코딩을 통해 변환을 거친 후 사용해야 한다. 

이와 관련된 프로토콜이 **Codable** 이다.

> **Encoding, Decoding 짚고가기**
>
> >  Encoding = 코드화 = 암호화 = 부호화
>
> 컴퓨터에서 인코딩은 동영상이나 문자 인코딩 뿐 아니라 사람이 인지할 수 있는 형태의 데이터를 약속된 규칙에 의해 컴퓨터가 사용하는 0과 1로 변환하는 과정을 통틀어 의미함.
>
> > Decoding = 역코드화 = 복호화
>
> 디코딩은 인코딩의 반대로서 사람이 이해 할 수 있도록 바꿔주는 것을 의미함.



### JSONDecoder

JSON 데이터를 `Codable` 프로토콜을 준수하는 `GroceryProduct` 구조체의 인스턴스로 디코딩하는 방법

```swift
struct GroceryProduct: Codable {
    var name: String
    var points: Int
    var description: String?
}

/// 스위프트 4 버전부터 """를 통해 여러 줄 문자열을 사용할 수 있습니다.
let json = """
{
    "name": "Durian",
    "points": 600,
    "description": "A fruit with a distinctive scent."
}
""".data(using: .utf8)!

let decoder = JSONDecoder()

do {
	let product = try decoder.decode(GroceryProduct.self, from: json)
	print(product.name)
} catch {
	print(error)
}
// ----- 출력
"Durian"
```

#### 웹에서 데이터 가져오기 - URL로 된 JSON, Parsing

1. String형태에 url 주소 저장한 후, 이를 url 객체로 변환
   - `guard-let`구문을 사용
2. Url 객체를 통해 JSON 파일 String으로 읽어오기
3. String 값을 data객체로 변환
4. Data 형태의 값을 JSONDecoder를 이용해 decode 해준다. 
5. 반환된 값을 원하는 객체에 담아준다. 

```swift
if let url = URL(string: "https://주소적어주기") {
           URLSession.shared.dataTask(with: url) { data, response, error in
            if let data = data {
                let jsonDecoder = JSONDecoder()
                do {
                    let parsedJSON = try jsonDecoder.decode(MusicData.self, from: data)
                    // print(parsedJSON.singer)
                } catch {
                    print(error)
                }
            }
           }.resume()
            
        }
```



### JSONEncoder

`Codable` 프로토콜을 준수하는 `GroceryProduct` 구조체의 인스턴스를 JSON 데이터로 인코딩하는 방법

```swift
struct GroceryProduct: Codable {
    var name: String
    var points: Int
    var description: String?
}

let pear = GroceryProduct(name: "Pear", points: 250, description: "A ripe pear.")

let encoder = JSONEncoder()
encoder.outputFormatting = .prettyPrinted

do {
	let data = try encoder.encode(pear)
	print(String(data: data, encoding: .utf8)!)
} catch {
	print(error)
}

// ----- 출력
 {
   "name" : "Pear",
   "points" : 250,
   "description" : "A ripe pear."
 }

// Tip : encoder.outputFormatting = .prettyPrinted 설정하면 들여쓰기를 통해 가독성이 좋게 출력해줍니다.
```





### References

- https://blckbirds.com/post/how-to-parse-json-with-swift-5/
- https://wan088.tistory.com/12
- https://woojin-hwang.github.io/ios-json/



