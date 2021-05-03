# Core Data

Persist or cache data on a single device, or sync data to multiple devices with CloudKit.

## Overview

Core Data를 사용하면, 디바이스에 permanent data를 저장할 수 있다. 

그러나 Core Data는 Database가 아니며, 데이터를 유지하기 위한 API도 아님

Core Data는 넓은 의미로 앱의 모델 계층이며, **객체 그래프를 관리하는 Framework**이다 



### Persistence

Core Data는 객체를 저장소에 매핑하는 세부 정보를 추상화하여 데이터베이스를 직접 관리하지 않고도 Swift 및 Objective-C의 데이터를 쉽게 저장할 수 있다.

![Flow diagram showing an app saving data to and loading data from a persistent store.](https://docs-assets.developer.apple.com/published/7d6b410668/95d28eec-4652-4824-bac8-a413ede649ea.png)



### Undo and Redo of Individual or Batched Changes

Core Data의 변경 사항을 추적하고 개별 또는 그룹으로 롤백 할 수 있으므로 앱에 실행 취소 및 다시 실행 지원을 쉽게 추가할 수 있음

![Figure showing a shake to undo gesture causing an element to be removed from a list.](https://docs-assets.developer.apple.com/published/6e6259c804/9ec0237d-0f5c-4f01-ac35-b6b55de236a9.png)



### Background Data Tasks

Perform potentially UI-blocking data tasks, like parsing JSON into objects, in the background. You can then cache or store the results to reduce server roundtrips.

백그라운드에서 JSON을 객체로 파싱하는 것과 같은 UI-blocking 데이터 작업을 수행함. 그런 다음 결과를 캐시하거나 저장하여 서버 왕복을 줄일 수 있음

![Flow diagram showing data from an endpoint populating objects in the background before updating the UI.](https://docs-assets.developer.apple.com/published/d090c20938/df1bcb18-0917-4fa0-a269-62e23d0ac3c9.png)



### View Synchronization

Core Data는 테이블 및 컬렉션 뷰에 데이터 소스를 제공하여 뷰와 데이터를 동기화 상태로 유지하는데도 도움이 된다.



### References

- https://developer.apple.com/documentation/coredata
- https://zeddios.tistory.com/987 [ZeddiOS]