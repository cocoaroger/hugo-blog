---
title: "Objective-C Guide Style"
date: 2017-08-26T10:57:31+08:00
keywords:
- iOS 代码规范
- Objective-C 代码规范
- OC
---

> Remember that code is read much more often than it is written, and that 80% of the lifetime cost of software goes to maintenance.

在 [搜布](www.isoubu.com) 与 [racechao](https://github.com/alfredcc) 一起整理

## 目录
* [参考和引用](#ref)
* [快捷键的使用](#keys)
* [命名规则](#name-style)
  - [变量命名](#var)
  - [常量命名](#const)
  - [类命名](#class-name)
  - [类属性定义](#ivar)
  - [方法的声明和定义](#function)
  - [方法中 {} 的位置](#curly-braces)
* [字面量](#literal)
* [布尔](#bool)
* [枚举类型](#enum)
* [Block](#block)
* [Protocols](#protocols)
* [代码组织](#code-organization)
* [Xcode 工程](#xcode)
* [Best Practices](#best-practices)


#### 参考和引用<a name = "ref"></a>
* [纽约时报 Objective-C 规范指南](https://github.com/NYTimes/objective-c-style-guide/blob/master/README_zh-Hans.md)

#### 快捷键的使用<a name = "keys"></a>

* 快速生成注释格式化：在声明的上一行 "option+command+/"
* 格式化代码：选中需要格式化的代码 "control+i"



### 命名规则<a name = "name-style"></a>
#### 变量命名<a name = "var"></a>

* 变量名应使用容易意会的全称，采用驼峰命名法，且首字母小写。
* 变量命名不允许出现中文拼音，应该使用英文对变量进行命名。

#### 常量命名<a name = "const"></a>

* `const ` 使用小写“k”作为前缀,首字母大写来分割单词。如: `kInvalidHandle`。
* 如果是NotificationName常量，不要使用k开头，以Notification结尾，如：UITextFieldDidBeginEditingNotification

```objective-c
    // 规范事例
    static const NSTimeInterval kRWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;

    // 不规范事例
    static const NSTimeInterval fadetime = 1.7;
```

#### 类命名<a name = "class-name"></a>

* 类名（包括`category name` 和 `protocol name`）的首字母大写，使用驼峰命名法命名。
* 在面向特定应用的代码中，类名应尽量避免使用前缀，每个类都使用相同的前缀影响可读性。
* 在面向多应用的代码中，推荐使用前缀。如:SCSendMessage
* Category Name 文件名使用原类名+扩展名的形式,如:NSObject+SCExtension.h/m 类名也使用该方式命名。

#### 类属性定义<a name = "ivar"></a>

如果变量可被外界访问：我们定义为“属性”（扩充了存取方法），若变量对外不可见我们则称之为“私有成员变量”

* 属性：使用 `@property ` 声明属性，可以方便的使用点语法
* 私有成员变量：@implementation 中直接添加类的私有成员变量，使用 `_` 作为前缀(如: `NSString * _varName;`)

> 原因：使用 \_  作为前缀，更容易在有代码自动补全功能的 IDE 中区分属性 (self.userInfo) 和 成员变量(\_userInfo)

```objective-c
// 规范事例
@interface Test : NSObject
    @property (copy, nonatomic) NSString *disc;
@end

@implementation ViewController {
    NSInteger _value;
}
```

[iOS 开发中的争议](http://blog.devtang.com/2015/03/15/ios-dev-controversy-1/)

#### 方法的声明和定义<a name = "function"></a>

* 方法名的首字母小写，且使用驼峰命名法命名，方法的参数使用相同的规则。
* 方法名+参数应尽量读起来像一句话
* getter的方法名和变量名应相同。不允许使用“get”前缀。 如

```objective-c
// 规范事例
- (id)delegate;

// 不规范事例
- (id)getDelegate;
```

* 非初始化方法，不能以`init` 作为前缀
* 在 `-` OR `+` 和返回值之间留1个空格，方法名和第一个参数间不留空格。方法名应该见名知意 如:

```objective-c
// 规范事例
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
}

// 不规范事例
-(BOOL)app:(UIApplication *)app options:(NSDictionary *)options {
}
```

* 当参数过长时，每个参数占用一行，以冒号对齐。如:

```objective-c
// 规范事例
- (void)doSomethingWith:(GTMFoo *)theFoo
                   rect:(NSRect)theRect
               interval:(float)theInterval {
        // do something
}

// 不规范事例
- (void)doSomethingWith:(GTMFoo *)theFoo rect:(NSRect)theRect interval:(float)theInterval {
        // do something
}
```

* 类方法以类的名字开头，并且首字母以小写开头，命名用驼峰命名法命名。 如：

```objective-c
// 规范事例
@interface Test: NSObject
    + (id)testWithDisc:(NSString *)disc;
@end
```

#### 方法中 {} 的位置<a name = "curly-braces"></a>

* 方法的第一个 `{` 紧接方法的最后一个字母，并且之间保留一个空格

```objective-c
// 规范事例
- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField {
    return YES;
}

// 不规范事例
- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField
{
    return YES;
}
或
- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField{
    return YES;
}
```

### 字面量<a name = "literal"></a>

- 关于字面量的解释请查看 <a href="http://clang.llvm.org/docs/ObjectiveCLiterals.html">http://clang.llvm.org/docs/ObjectiveCLiterals.html</a>

```objective-c
// 规范事例
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;

// 不规范事例
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

> 原因：
>
> 1. 字面值在静态编译时就会报错，如将 `nil` 值传入 `NSArray` 或 `NSDictionary` 例如 `NSArray *array = [@"cat",nil];`    ❌
> 2. 使用字面值代码更加简洁，可读性更高

### 布尔<a name = "bool"></a>

因为 nil 解析为 NO，所以没有必要在条件中与它进行比较。永远不要直接和 YES 进行比较，因为 YES 被定义为 1，而 BOOL 可以多达 8 位。
这使得整个文件有更多的一致性和更大的视觉清晰度。

```objective-c
// Bool判断
// 规范事例
if (isAwesome) {

}
// 不规范事例
if (isAwesome == YES) {
}
if (isAwesome == true) {
}

// 对象空值判断
// 规范事例
if (someObject) {
    // do something
}
// 不规范事例
if (someObject != nil) {
    // do something
}
```
如果一个 BOOL 属性名称是一个形容词，属性可以省略 “is” 前缀，但为 get 访问器指定一个惯用的名字，例如：

```objective-c
@property (assign, getter=isEditable) BOOL editable;
```
### 枚举类型<a name = "enum"></a>

当使用 enum 时，建议使用新的基础类型规范，因为它具有更强的类型检查和代码补全功能。现在 SDK 包含了一个宏来鼓励使用使用新的基础类型 - NS_ENUM()

#### 例如：

```objective-c
typedef NS_ENUM(NSInteger, SCOrderStatus) {
    SCOrderStatusWaitToPay,
    SCOrderStatusWaitToDeliver
};
```

###  Block<a name = "block"></a>

```objective-c
// 规范事例
[UIView animateWithDuration:1.0 animations:^{
    // do something
} completion:^(BOOL finished) {
    // do something
}];

// 不规范事例
[UIView animateWithDuration:1.0
                 animations:^{
                     // do something
                 }
                 completion:^(BOOL finished) {
                     // do something
}];
```

### Protocols<a name = "protocols"></a>
* 类型标示符、代理名称、尖括号间留一个空格。 如:

```objective-c
// 规范事例
@interface Test : NSObject <UITableViewDelegate>
@end
```

* 如果类声明中包含多个protocal,每个protocal占用一行,缩进4个字符。如:

```objective-c
@interface Test : NSObject <UITableViewDelegate,
    NSCoding,
    NSCopying> {
}
@end
```

### 注释
* 尽量在方法或变量的上一行写注释，尽量减少无意义的注释。在每个类前也要尽量添加关于类的说明的注释。
* 注释格式如下：

```objective-c
// 规范事例
/**
 找回密码

 @param phone 手机号
 @param password 新密码
 @param code 验证码
 @param complete 回调
 */
+ (void)findPasswordWithPhone:(NSString *)phone
                     password:(NSString *)password
                         code:(NSString *)code
                     complete:(Complete)complete;
```

### 关键字copy，assign，retain，weak，strong的使用
* 在ARC中，使用strong替代retain

* copy使用在 NSString、NSMutableString、Block中
* assign使用在基本数据类型中
* weak使用在代理或者UI控件
* strong使用在除了上面3条的所有情况


## 代码组织
使用 `pragma mark -` 对方法进行分组以及对 `protocol/delegate` 的实现方法前面进行申明

```objective-c
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)viewDidLoad {}
- (void)dealloc {}
...

#pragma mark - Custom Accessors

- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public Methods

- (void)publicMethod {}

#pragma mark - Private Methods

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate
```

> Tips: 每一个 `delegate` 都把对应的 `protocol` 名字带上，这样有个好处就是，当其他人阅读一个他并不熟悉的Delegate实现方法时，他只要按住command然后去点这个protocol名字，Xcode就能够立刻跳转到对应这个Delegate的protocol定义的那部分代码去，就省得到处找了。
> <br/>

### Xcode 工程<a name = "xcode"></a>
为了避免文件杂乱，物理文件应该保持和 Xcode 项目文件同步。Xcode 创建的任何组（group）都必须在文件系统有相应的映射。为了更清晰，代码不仅应该按照类型进行分组，也可以根据功能进行分组。

自动创建：
对于现有的大量的Group，手动一个一个创建实在不方便，还好有个命令行工具：`synx`，直接在工程根目录运行`synx XXX.xcodeproj` 就可以自动为Group创建物理文件夹。
当然，CocoaPods管理的库要重新pod install一次，手动添加的Framework也要重新添加。

### Best Practices<a name = "best-practices"></a>
* Always copy blocks when stored
* 多使用 `static const` 修饰常量的，代替 `#define` 的定义方式，因为前缀存在类型检查。

```objective-c
static const CGFloat kFooBar = 123.0f;
```

* 在 .h 头文件中避免不必要的 import
* 使用 `@class ClassName` 代替 `#import ClassName.h`
* 防止子线程访问UI
* UIKit的大部分对象都不是线程安全的，所有继承自UIResponder的类都需要在主线程操作，如果在子线程更改了这些UI对象就会导致未知道的行为，比如随机出现丢失动画、页面错乱甚至crash。
* 代理协议中必须实现的方法要用@required标明，不一定要实现的方法要用@optional标明
* 使用NSInteger或者是NSUInteger替代int/long/unsign int/unsign long
* 使用CGFloat替代float
