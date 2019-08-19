
# Olympic Objective-C Coding Style Guide
## 间距
+ 一个缩进使用 4 个空格，永远不要使用制表符（tab）缩进。。
+ 方法的大括号和其他（`if`/`else`/`switch`/`while` 等等）大括号始终和声明在同一行开始，在新的一行结束。
##### 推荐：
```
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}
```
##### 反对：
```
if (user.isHappy) {
  //Do something
} 
else
 {
  //Do something else
}
```
+ 方法之间应该正好空一行，这有助于视觉清晰度和代码组织性。在方法中的功能块之间应该使用空白分开，但往往可能应该创建一个新的方法。
## 条件判断
条件判断主体部分应该始终使用大括号括住来防止出错，即使它可以不用大括号（例如它只需要一行）。
##### 推荐：
```
if (!error) {
    return success;
}
```
##### 反对：
```
if (!error) 
    return success;
```
##### 或：
```
if (!error) return success;
```
## 三目运算符
+ 三目运算符，`? :` ，只有当它可以增强代码清晰度时使用。单一的条件优先考虑使用。多条件时通常使用 if 语句会更易懂。
##### 推荐：
```
result = a > b ? x : y;
```
##### 反对：
```
result = a > b ? x = c > d ? c : d : y;
```
## 方法
+ 在方法签名中，在 -/+ 符号后应该有一个空格。方法片段之间也应该有一个空格。
+ 方法名: 多个参数名前的方法要有描述性的关键字,并且不要包含and字段。
##### 推荐：
```
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```
## 方法命名
+ 小写第一个单词的首字符，大写随后单词的首字符，通常不使用前缀。有两种例外情况：
1、方法名以广为人知的大写字母缩略词（如TIFF or PDF）开头；
2、私有方法可以使用统一的前缀来分组和辨识。
表示对象行为的方法，名称以动词开头
##### 推荐
```
- (void)invokeWithTarget:(id)target:
- (void)selectTabViewItem:(NSTableViewItem *)tableViewItem
```
+ 方法返回接收者的某个属性，直接用属性名称命名。
##### 推荐
```
- (CGSize)cellSize;
```
+ 参数前面的单词要能描述该参数
##### 推荐
```
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag; 
```
## 方法分组
+ 使用 `#pragma mark - `对方法进行分组
##### 推荐
```
#pragma mark - 生命周期
- (void)viewDidLoad {
    [super viewDidLoad];
}

- (void)viewWillAppear:(BOOL)animated {
    [super viewWillAppear];
}

#pragma mark - 初始化对象懒加载
- (NSMutableArray *)dataSource{
    if (!_dataSource) {
    _dataSource = [NSMutableArray array];
    }
    return _dataSource;
}

- (NSMutableArray *)tempDataArray{
    if (!_tempDataArray) {
    _tempDataArray = [NSMutableArray array];
    }
    return _tempDataArray;
}
```
## 变量
+ 变量名应该尽可能命名为描述性的。除了 `for()` 循环外，其他情况都应该避免使用单字母的变量名。
+ 星号表示指针属于变量，例如：`NSString *text` 不要写成 `NSString* text` 或者 `NSString * text` ，常量除外。
+ 尽量定义属性来代替直接使用实例变量。除了初始化方法（`init`， `initWithCoder:`，等）， `dealloc` 方法和自定义的 setters 和 getters 内部，应避免直接访问实例变量。
##### 推荐：
```
@interface NYTSection : NSObject

@property (nonatomic) NSString *headline;

@end
```
##### 反对：
```
@interface NYTSection : NSObject {
    NSString *headline;
}
```
## 常量
+ 常量首选内联字符串字面量或数字，因为常量可以轻易重用并且可以快速改变而不需要查找和替换。常量应该声明为 `static` 常量而不是 `#define` ，除非非常明确地要当做宏来使用。
#####推荐
```
static NSString * const LenzAboutViewControllerCompanyName = @"The Lenz Company";

static const CGFloat LenzImageThumbnailHeight = 50.0;
```
##### 反对
```
#define CompanyName @"The Lenz Company"

#define thumbnailHeight 2
```
## 宏定义
+ 全部大写，单词间用_分隔（不带参数）
```
#define IS_IPHONE_VERSION @"9.0"
```
+ 以字母k开头，后面遵循大驼峰命名（不带参数）
```
#define kStatusCode @"0000"
```
## 字面量
每当创建` NSString`，`NSDictionary`，`NSArray`和`NSNumber` 类的不可变实例时，都应该使用字面量。
##### 推荐
```
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingZIPCode = @10018;
```
##### 反对
```
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingZIPCode = [NSNumber numberWithInteger:10018];
```
## 图片命名
+ 命名规则的基本思想是把文件名分成三部分，第一部分是图片的逻辑归属分类，第二部分是图片的表现内容，第三部分是图片的内容类型，有些图片还会有第四部分，表示图片表现的状态。
1、用英文命名，不用拼音；
2、每一部分用下划线分隔；
3、图片名中两倍图在名字最后要加@2x，三倍图在名字最后要加@3x。
##### 推荐
+ `home_imageview_banner@2x.png`
`tab_button_search_normal@2x.png`
`tab_button_news_normal@3x.png`
## 布尔
+ 因为 nil 解析为 NO，所以没有必要在条件中与它进行比较。永远不要直接和 YES 进行比较，因为 YES 被定义为 1，而 BOOL 可以多达 8 位。
##### 推荐
```
if (!someObject) 

if (isAwesome)

if (![someObject boolValue])
```
##### 反对
```
if (someObject == nil) 

if ([someObject boolValue] == NO)

if (isAwesome == YES) // 永远别这么做
```
## 注释
+ 类的注释写在当前类的顶部
+ 属性的注释写在属性的上方，用`///`注释
##### 推荐
```
/// 刷新按钮
@property (nonatomic, strong) UIButton *refreshBtn;
```
+ 对于`.h`文件中的方法注释，一律按快捷键 command+option+/。三个快捷键解决。
## 推荐
```
/**
 获取时间链发布时间

 @param timeStamp 时间戳（毫秒）
 @return 展示时间
 */
+ (NSString *)getHotNewsPublishTime:(NSString *)timeStamp;
```
