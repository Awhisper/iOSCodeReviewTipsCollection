#reviewcode.cn 平台部分案例整理
我是大神们的搬运工

##彦祖大神的codeReview平台
@叶孤城___ 大神搞了一个提供邀请业内大神付费为你的项目进行CodeReview的平台，产出一份高质量的review报告。[www.reviewcode.cn](www.reviewcode.cn)

###为什么要做CodeReview？
引用大神在网站中的一句话

>因为 Code Review 是一种最快捷有效的方式让你清楚地知道“好的代码是怎样写出的”。不知道你们有没有这样的经历。

>知道如何完成一个功能，或者完成一个组件。但是碰到稍微复杂的逻辑和业务，就会很容易的让代码变得一团糟。书中常常提及的解耦、分拆复杂逻辑都似乎变成了纸上谈兵，无从下手。又或者，总觉得自己的代码哪里不对劲，和高手们写的简洁、易懂、风格优雅的代码总是有似乎逾越不了的鸿沟。


我个人是觉得，代码能力的培养，代码质量的提升，不仅仅是我又学到了什么新技术，掌握了什么nb的黑科技。

更离不开对自己写出的每一句代码的反复challenge，小到命名规范，数字常量，大到模块设计，项目结构，无处不存在着可以不断优化和提升的细节。

看看行业的高手大神们是怎么思考和写码的，看看他们在跟你思考一模一样的问题的时候，他们视野他们的角度，学习，汲取，不断地提升自己

>观一叶而知秋，道不远人即为此

代码的`道`，其实就在这些点点滴滴的细节所汇聚而成的`艺术品`里（咳...装X了...跑题了...）

##平台案例整理

可能不见得每个人都要把自己所有的项目，扔到平台上让大神们review，但是我们可以进行归纳总结，在那些大神们的`高质量review报告`中，归纳和总结我们自己需要的，汲取养分。

更何况这些总结，每一个都包含着真实的代码案例，优化方案，以及原因详解，比我们每天看设计模式那些抽象的理念，名词，要接地气的多

###我不是大神，我只是大神的搬运工
(农夫山泉的广告词...咳...装X了...跑题了...)

目前CodeReview平台上已经有了超级详尽的10篇review报告，每一个都是实打实的干活，所以我就搬运一下，把他们case by case 的review报告，梳理归类一下，换个形式进行总结和学习

###一. 命名规范

在10篇review报告中有3篇提到了命名规范这个事情

- [一些代码建议](http://www.reviewcode.cn/article.html?reviewId=8)
- [要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)
- [命名的艺术](http://www.reviewcode.cn/article.html?reviewId=2)

其实关于命名规范，有很多现成的方法论和规范了，各种语言，对于类，函数，变量，等等，一查都能查到很多。我觉得这里面最重要的意义是让你写出的东西别人好读，好认，不要靠猜。

大神们给出了很多建议

- 前缀：建议所有类名、enum 定义、typedef 类型定义，都加上前缀（prefix）
- 拼写错误：不用多说了
- 命名规范：建议尽可能统一，就算多人团队合作，在开发中统一一下习惯总是好的。
 	- 比如到底是_分割还是驼峰大小写分割单词？（建议驼峰）
 	- 是否对返回值的类型描述写入函数名，方法名里面？（建议写像苹果系统Api）


[命名的艺术](http://www.reviewcode.cn/article.html?reviewId=2)这篇报告更是着重的对命名规范从四个方向进行了很深入的剖析

- 变量的命名
- 代理的命名
- 图片资源的命名
- 方法的命名

###二.编码细节
写代码的时候，有时候很细微的一行代码，稍加变化，稍加处理，可能就会有很多性能，可读性，扩展性等得提升，在10篇review报告中，有太多这样高质量的编码细节干活。

####1）数字与常量

- [要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)
- [关于性能的一些问题](http://www.reviewcode.cn/article.html?reviewId=7)
- [好的代码习惯](http://www.reviewcode.cn/article.html?reviewId=10)
- [一些优化代码结构的方法](http://www.reviewcode.cn/article.html?reviewId=4)

都提到了`数字`，比如

# 

	UILabel *infoLabel = [[UILabel alloc] initWithFrame:CGRectMake(0, 241, 320, 28)];
	
这个还算好的，再看看这个

	CGRect rect = CGRectMake(12.2+(page-1)*320+42.5*(i%7),((totalRows-1)%3)*55+2,42.5,42.5);
	
	
大神们建议这么使用

	static const CGFloat kTagHeight = 30.0f;
	static const CGFloat kTagLabelWidthInset = 16.0f;


另外，不建议用宏，具体有兴趣大家可以看简书的这个帖子 ，[iOS中关于宏定义与常量的使用](http://www.jianshu.com/p/c941e37a8a1d)，简单的说就是宏会增加编译速度

同理一些字符串常量等，都建议使用 这样的定义

	static NSString *const kcircleModelDataCategoryName = @"categoryName";

####2）监听通知的位置

[一些优化代码结构的方法](http://www.reviewcode.cn/article.html?reviewId=4)中提到

>有人在willAppear和Disappear中添加通知，这样极容易出现问题。因为willAppear和Disappear出现的顺序并不一定是一对一的。所以有可能造成多次添加，多次移除通知。

大神们建议这么使用
>建议在viewDidLoad里添加通知。在dealloc里移除通知。

####3） 私有成员 or Property

[话谈 iOS 目录结构的划分](http://www.reviewcode.cn/article.html?reviewId=9)中提到的一个问题

	@interface PartyViewController ()

	@property (weak, nonatomic) IBOutlet UITableView *partyTableView;
	@property (strong,nonatomic) NSMutableArray *partys;
	@end
	
	@implementation PartyViewController{
	
	    NSMutableArray *lodedIndex;
	}
	
到底该用哪一个？

大婶们的建议是
>无论如何，应该一致，应该统一风格。建议这里用 property 。因为 @IBOutlet ，从 IB 拖出来的属性用的就是 property ，所以统一用 property 较好。
	
关于这个，其实在开发中有一定的争议的，有兴趣的可以看一下唐巧老师的这篇文章，[开发中得争议](http://blog.devtang.com/2015/03/15/ios-dev-controversy-1/)

####4） typedef block
[话谈 iOS 目录结构的划分](http://www.reviewcode.cn/article.html?reviewId=9) 提到代码中多次使用的block，诸如`(void (^)(NSError *error))`等，可以统一进行声明，不要每次都手打完整block定义

好处是

>还可以用上 Xcode 的自动补全功能，当你输入 Fa 的时候， FailureBlock 的提示就出来了。用 (void (^)(NSError *error)) 就没有自动补全了，每次都要手工输入一遍，很麻烦

####5） 数字类型

[话谈 iOS 目录结构的划分](http://www.reviewcode.cn/article.html?reviewId=9)中提到了3个问题

- 用 int 还是 NSInteger
- 尺寸变量统一用 CGFloat
- 选用正确的类型，让编译器能静态检查


第一个问题

>可以注意到 apple 的 UIKit 等代码一般都是用的 NSInteger。NSInteger 在 32位系统是 int ，64位系统是 long 。Apple 把它用在函数的参数处，和返回的地方。为什么？因为函数是需要跟其它代码或其它平台的代码交流互动的，所以是 int 还是 long 很重要。系统的代码用的是 NSInteger 的话，你的用了 int 的话，可能不够大而造成崩溃。

还是建议NSInteger

第二个问题 
> 一开始看到 `int padding = 1` 后，不知道它是干嘛的。因为附近没有它的代码，看到后面才知道的。所以声明类型为 CGFloat ，更容易知道它是来定义尺寸距离的。

为什么建议这样，CG开头是CoreGraphic的简写，我们开发也会发现CGFloat 是需要 import `UIKit`的，从名字定义上，他是与现实UI有关的

第三个问题

具体可以看链接里的案例

简单的说就是，很多NSInterger等数值属性，不要把他定义成NSNumber，因为编译器在发现你对integer变量赋值float变量的时候会自动报错，是一个自动纠错的功能，如果定义成了NSNumber，用语法糖@（float）去转换，就不能自动纠错了

####6）属性修饰符建议
[好的代码习惯](http://www.reviewcode.cn/article.html?reviewId=10)中提到

>在arc中，弱引用最好使用weak，来避免野指针的出现，weak可以在指向的对象dealloc的时候自动置为nil。

>在arc中强引用尽量使用strong，当然这里strong和retain的作用是一样的，但是为了保持代码的一致性，这里推荐使用strong。

具体可以看链接中得案例

####7） 字面量语法

[好的代码习惯](http://www.reviewcode.cn/article.html?reviewId=10)中提到

	_comps.items = [NSArray arrayWithObjects:_photoBarButton, _mediaBarButton, _alarmBarButton, _brushBarButton, _voiceBarButton, _doneBarButton, nil];

字面量语法

	_comps.items = @[_photoBarButton, _mediaBarButton, _alarmBarButton, _brushBarButton, _voiceBarButton, _doneBarButton];
	
>这种做法不仅简单，还更加安全。假如当中的_alarmBarButton为nil，那么通过第一种写法，数组还是会创建出来，只不过数组内只有2个对象，原因在于，“arrayWithObjects:”方法会依次处理各个参数，直到发现nil为止，而第二种写法会在插入nil指针的时候抛出异常，令程序终止运行，这比创建好数组后才发现数组内的元素个数少了要好很多。异常往往能更快地发现错误。

###三.设计思路
