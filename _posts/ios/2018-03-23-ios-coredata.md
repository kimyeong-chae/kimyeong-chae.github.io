---
layout: post
title:  "Core Data CRUD 코드 예제"
date:   2018-03-23 01:22:21 +0900
categories: ios
author : yckim
---


### 데이터 추가 & 수정

```
// 앱 델리게이트 객체 참조
let appDelegate = UIApplication.shared.delegate as! AppDelegate

// 관리 객체 컨텍스트 참조
let context = appDelegate.persistentContainer.viewContext

// 관리 객체 생성, 수정일 경우 관리 객체를 파라미터로 받아와 이단계를 생략.
let object = NSEntityDescription.insertNewObject(forEntityName:"엔티티명", into: context)

object.setValue(변수명, forKey: "엔티티 Attribute명")

do {
  try context.save()
} catch {
  context.rollback()
}
```


### 데이터 삭제

```
let appDelegate = UIApplication.shared.delegate as! AppDelegate
let context = appDelegate.persistentContainer.viewContext

// 관리 객체 컨텍스트에서 삭제
context.delete(관리객체변수)

do {
	try context.save()
} catch {
	context.rollback()
}
```

### 데이터 조회

```
let appDelegate = UIApplication.shared.delegate as! AppDelegate
let context = appDelegate.persistentContainer.viewContext

// 가져올 엔티티 정의
let fetchRequest = NSFetchRequest<NSManagedObject>(entityName:"엔티티명")

// 정렬 설정
let sort = NSSortDescriptor(key: "regdate", ascending: false)
fetchRequest.sortDescriptors = [sort]

// 데이터 가져오기
let result = try! context.fetch(fetchRequest)
```
