# SyrupAd Objective-C Style Guide

이 스타일 가이드는 SyrupAd팀의 iOS 코딩 규칙을 설명합니다.


## <a name='Introduction'>소개</a>

이 문서는 팀내 Objetivce-C의 코딩 규칙을 정의하여 제각각 다른 스타일의 팀원들이 불필요하게 코드를 수정하지 않도록 유도하고(자동 줄맞춤 등의 기능으로 인해), 이후 작업하는 모든 코드들에도 똑같이 적용하여 일관성 있는 코드로 유지되도록 만들어졌습니다. 다음과 같은 문서들을 참조하였습니다.

* [Github objective-c-style-guide](https://github.com/github/objective-c-style-guide.git)
* [NYTimes objective-c-style-guide](https://github.com/NYTimes/objective-c-style-guide.git)
* [raywenderich objective-c-style-guide](https://github.com/raywenderlich/objective-c-style-guide.git)



## <a name='dot-notation-syntax'>Dot-Notation Syntax</a>

* 점 표기법은 항상 **프로퍼티** 값에 접근하거나 변경할 때 사용합니다. 
* 대괄호 표기법은 그 외의 모든 상황에서 사용합니다.
	* ex) 팩토리 메서드, getter 메서드 사용

**For example:**
```objc
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Not:**
```objc
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## <a name='spacing'>Spacing</a>

* 들여쓰기는 탭을 사용합니다. 스페이스로 들여쓰지 않습니다.
* 파일의 끝에 새 줄을 추가합니다.
* 메소드 중괄호와 다른 중괄호 (`if`/`else`/`switch`/`while` etc.)는 항상 같은 줄에서 문을 열고 새로운 줄에서 닫습니다.
	* else if, else는 해당 괄호의 끝에서 시작합니다.

**For example:**
```objc
if (user) {
	// Do something
} else if (user.isHappy) {
	// Do something else if
} else {
	// Do something else
}
```

* 로직의 이해와 단위를 구분하기 위해 적절하게 빈 줄을 삽입합니다. 
* 각 코드의 끝에는 공백(들여쓰기, 스페이스 등)을 남기지 않습니다.

## <a name='methods'>Methods</a>

메소드 서명에 범위(-/+ 기호)뒤에 공백을 추가합니다. 메서드 반환값 표기 뒤에는 메서드명을 붙여서 씁니다.

**For Example**:
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```

**Not:**
```objc
-(void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void) setExampleText:(NSString *)text image:(UIImage *)image;
```

## <a name='variables'>Variables</a>

* 변수는 서술이 가능하도록 명명되어야 합니다. 한 글자 변수는 `for()` 문을 제외하곤 쓰지 않습니다.
* 또한 상수의 경우를 제외하고, 포인터를 나타내는 별표는 변수에 붙입니다. 

**For example:**

```objc
@interface TadCore: NSObject
@property (nonatomic) NSString *clientId;
@end
```

**Not:**

```objc
@interface TadCore : NSObject {
    NSString* clientId;
    NSString * clientId;
}
```

## <a name='conditionals'>Conditionals</a>

한 줄짜리 조건문의 괄호는 생략하지 않습니다.

**For example:**
```objc
if (!error) {
    return success;
}
```

**Not:**
```objc
if (!error)
    return success;
```

or

```objc
if (!error) return success;
```


### <a name='ternary-operator'>Ternary Operator</a>

3항 연산자 ?는 명료함과 코드 간결함을 높일 때 사용합니다. 단일 조건을 비교할 때만 사용합니다. 일반적으로 다중 조건 비교는 if 문 또는 인스턴스 변수로 코딩합니다.

**For example:**
```objc
result = a > b ? x : y;
```

**Not:**
```objc
result = a > b ? x = c > d ? c : d : y;
```

## <a name='literals'>Literals</a>

`NSString`, `NSDictionary`, `NSArray`, `NSNumber` 리터럴은 불변 인스턴스 객체를 생성하는데 사용합니다. 

**For example:**

```objc
NSArray *keywords = @[@"iPhone", @"iPad", @"Macbook"];
NSDictionary *productManagers = @{@"iPhone" : @"Kate", @"iPad" : @"Kamal", @"Mobile Web" : @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *userId = @10018;
```

**Not:**

```objc
NSArray *keywords = [NSArray arrayWithObjects:@"iPhone", @"iPad", @"Macbook", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingZIPCode = [NSNumber numberWithInteger:10018];
```

## <a name='setter-getter'>Setter, Getter</a>
프로퍼티의 Setter와 Getter는 다음과 같이 작성합니다.

**For example**
``` objc
[user setName:@"name"];
user.name;
```

**Not**
``` objc
user.name = @"name";
[user name];
```

## <a name='naming'>Naming</a>

애플 명명 규칙은 가능하면 준수해야 하며, 특히 [메모리 관리 규칙](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html)([NARC](http://stackoverflow.com/a/2865194/340508))과 관련있습니다.

길고 상세한 메소드와 변수명이 좋습니다.

**For example:**

```objc
UIButton *settingsButton;
```

**Not**

```objc
UIButton *setBut;
```

세 글자 접두사(예, `TAD`)는 클래스 이름과 상수에 사용하지만, Core Data entity 이름에는 생략될 수 있습니다. 상수는 대문자와 명확성을 위한 연관된 클래스 이름을 접두사로 하는 모든 단어를 낙타 표기법으로 해야 합니다.

**For example:**

```objc
static const NSTimeInterval TADArticleViewControllerNavigationFadeAnimationDuration = 0.3;
```

**Not:**

```objc
static const NSTimeInterval fadetime = 1.7;
```


## <a name='booleans'>Booleans</a>
`nil`은 `NO`로 해석되기 때문에 추가적으로 표시하지 않습니다.

**For example:**

```objc
if (!someObject) {
}
```

**Not:**

```objc
if (someObject == nil) {
}
```

-----

**For a `BOOL`, here are two examples:**

```objc
if (isAwesome)
if (![someObject boolValue])
```

**Not:**

```objc
if ([someObject boolValue] == NO)
if (isAwesome == YES) // Never do this.
```

-----

예를 들어 `BOOL` 프로퍼티 이름이 형용사로 나타내면, 프로퍼티는 “is” 접두사는 생략할 수 있지만 get 접근자는 기존 이름을 지정합니다:

```objc
@property (assign, getter=isEditable) BOOL editable;
```

[Cocoa Naming Guidelines](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE)에서 가져온 글과 예제입니다.

## <a name='singletons'>Singletons</a>

싱글톤 객체는 공유 인스턴스를 생성하기 위해 쓰레드 세이프 패턴을 사용합니다.

```objc
+ (instancetype)sharedInstance {
   static id sharedInstance = nil;

   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
      sharedInstance = [[self alloc] init];
   });

   return sharedInstance;
}
```

이것은 [가끔 원인이 되는 충돌](http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html)을 방지할 수 있습니다.
