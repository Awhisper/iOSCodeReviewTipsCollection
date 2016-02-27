#reviewcode.cn 平台部分案例整理
我是大神们的搬运工

##彦祖大神的codeReview平台
@叶孤城___ 大神搞了一个提供邀请业内大神付费为你的项目进行CodeReview的平台，产出一份高质量的review报告。[www.reviewcode.cn](www.reviewcode.cn)

##平台案例整理

可能不见得每个人都要把自己所有的项目，扔到平台上让大神们review，但是我们可以进行归纳总结，在那些大神们的`高质量review报告`中，归纳和总结我们自己需要的，汲取养分。

更何况这些总结，每一个都包含着真实的代码案例，优化方案，以及原因详解，比我们每天看设计模式那些抽象的理念，名词，要接地气的多

我不是大神，我只是大神的搬运工

(农夫山泉的广告词...咳...装X了...跑题了...)

目前CodeReview平台上已经有了超级详尽的10篇review报告，每一个都是实打实的干活，所以我就搬运一下，把他们case by case 的review报告，梳理归类一下，换个形式进行总结和学习

###为什么要做CodeReview？
引用大神在网站中的一句话

>因为 Code Review 是一种最快捷有效的方式让你清楚地知道“好的代码是怎样写出的”。不知道你们有没有这样的经历。

>知道如何完成一个功能，或者完成一个组件。但是碰到稍微复杂的逻辑和业务，就会很容易的让代码变得一团糟。书中常常提及的解耦、分拆复杂逻辑都似乎变成了纸上谈兵，无从下手。又或者，总觉得自己的代码哪里不对劲，和高手们写的简洁、易懂、风格优雅的代码总是有似乎逾越不了的鸿沟。


我个人是觉得，代码能力的培养，代码质量的提升，不仅仅是我又学到了什么新技术，掌握了什么nb的黑科技。

更离不开对自己写出的每一句代码的反复challenge，小到命名规范，数字常量，大到模块设计，项目结构，无处不存在着可以不断优化和提升的细节。

看看行业的高手大神们是怎么思考和写码的，看看他们在跟你思考一模一样的问题的时候，他们视野他们的角度，学习，汲取，不断地提升自己

>观一叶而知秋，道不远人即为此

代码的`道`，其实就在这些点点滴滴的细节所汇聚而成的`艺术品`里（咳...装X了...跑题了...）


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

同理一些字符串`常量`等，都建议使用 这样的定义

	static NSString *const kcircleModelDataCategoryName = @"categoryName";

####2）监听通知的位置

[一些优化代码结构的方法](http://www.reviewcode.cn/article.html?reviewId=4)

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
[好的代码习惯](http://www.reviewcode.cn/article.html?reviewId=10)

>在arc中，弱引用最好使用weak，来避免野指针的出现，weak可以在指向的对象dealloc的时候自动置为nil。

>在arc中强引用尽量使用strong，当然这里strong和retain的作用是一样的，但是为了保持代码的一致性，这里推荐使用strong。

具体可以看链接中得案例

####7） 字面量语法

[好的代码习惯](http://www.reviewcode.cn/article.html?reviewId=10)

	_comps.items = [NSArray arrayWithObjects:_photoBarButton, _mediaBarButton, _alarmBarButton, _brushBarButton, _voiceBarButton, _doneBarButton, nil];

字面量语法

	_comps.items = @[_photoBarButton, _mediaBarButton, _alarmBarButton, _brushBarButton, _voiceBarButton, _doneBarButton];
	
>这种做法不仅简单，还更加安全。假如当中的_alarmBarButton为nil，那么通过第一种写法，数组还是会创建出来，只不过数组内只有2个对象，原因在于，“arrayWithObjects:”方法会依次处理各个参数，直到发现nil为止，而第二种写法会在插入nil指针的时候抛出异常，令程序终止运行，这比创建好数组后才发现数组内的元素个数少了要好很多。异常往往能更快地发现错误。

###三.设计思路
####1）公有私有混乱
[要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)

具体案例可以看Link中得细节，大致思路是尽可能的减少接口在头文件中所暴露出来的属性和方法，头文件要尽可能的简洁

如果有可能也尽量避免，一个头文件中出现多个类声明

>头文件里地方小，塞到一处并不好。 外部对象都知道，安全问题可不小

####2）消息通知满天飞
[要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)

通知虽好，但也不要贪杯啊。

>看起来轻松，只是 post 了一下就搞定了，但是在 Debug 的时候有点麻烦。尤其是如果有多个 Observer ，改动的时候牵一发而动全身。如果真的是有这样使用的必要倒也罢了，但是本来一个 block 或者 delegate 就能简单清晰的解决，现在却被搞得这么繁重，实在是没有必要。

我觉得明确使用通知的场景，在不需要一对多的情况下，路径不算远的2个模块，完全可以通过delegate，或者block解决

####3）单个对象多职责
[要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)

同一个一个模块

- 上能和服务器聊天，上传聊天消息同步聊天记录
- 下能做本地缓存管理，增删改查样样精通
- 弹窗提醒，上传进度，完成提示，亦是轻松拿下。
- 以至于你改着改着不知不觉都会走到这里，因为它处理了太多太多的业务逻辑，每次 DEBUG 追杀断点回到这里，都像是一场久别重逢时的相遇，似曾相识

>一人做事一人当，切忌都往类里装。 开发人员干的爽，维护人员很受伤。

####4）盲目新增功能
[要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)

具体案例可以看Link中的细节，简单描述下就是，随着项目的迭代，一个小功能点，多一个标记位，再来一个小功能点，又多一个标记位，随着业务迭代下去，标记位越来越多，如果这里面涉及到逻辑上的关联，一单有个标记位得特殊处理一下，那N个`if`嵌套的场景，简直是`画美不看`

新增的业务需求，还是要经常和老功能进行梳理和总结，该合并该梳理的都要重新和老代码里一起整合，切记直接拍脑袋上手直接添加功能

####5）滥用委托
[要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)

[封装一个UI控件的范例](http://www.reviewcode.cn/article.html?reviewId=5)

都提到了在处理回调的时候，委托或者block的2个方式的对比

>所谓悲哀就是，当程序员发现一个 delegate 就能访问上级的对象，于是便把各种需要通知上级的事情都放在了委托方法里，尽管这些事情与委托本身无关，但是为了实现功能已经不在意这些所谓的设计与美观

>可以考虑用block来传递数据源和响应事件，这样封装的view在代码的连贯性上更好一些

简单的说结合具体案例，恰当的采用委托或者block来实现

####6）静态DataSource
[一些优化代码结构的方法](http://www.reviewcode.cn/article.html?reviewId=4)

开发中难免会遇到很多静态的几乎很少变化的tableView界面

图省事的人直接在代码里 switchCase  一行行的硬编码，写死了整个tableview的界面

还是推荐使用plist，用代码从数据源中读取数据，从而进行展示

>这样，后续迭代版本的内容只需要修改plist文件的内容就可以了。而不需要在代码中修改逻辑。

####7）使用orm
[一些优化代码结构的方法](http://www.reviewcode.cn/article.html?reviewId=4)

很多人都是这么做的

不要在解析网络等数据的时候，手写解析过程，采用`mantle`or`JsonModel`等框架来做这些事情

####8）构建易于测试的模块
[一些优化代码结构的方法](http://www.reviewcode.cn/article.html?reviewId=4)
[如何打造令人愉悦的开发环境](http://www.reviewcode.cn/article.html?reviewId=1)

都提到了，尽量在开发中设计易于测试的模块。
众多功能杂糅在一个类里面是不利于测试的，写一个超大函数，干了很多功能也是不利于编写自动化测试的
后面还会提到，随着项目的逐渐扩大，保持至健壮的自动化测试+持续集成，才是一个健康的项目结构

####9）不要想当然的使用tableView

[不要想当然的使用tableView](http://www.reviewcode.cn/article.html?reviewId=6)

- 不要试图过分的复用一个TableViewController
- 一定要复用的场景
	- 用switch来区分场景，用不同的tableview进行处理
	- 将数据源的判断逻辑，不同的tableview类给自己处理自己的`delegate` or `datasource`
	- 这样多路复用的选择其实就发生在了返回tableView的操作里，可以避免在控制器中出现臃肿的代码
- 不要试图滥用Cell的重用机制

####10）圆角
[关于性能的一些问题](http://www.reviewcode.cn/article.html?reviewId=7)

详细可以看关于离屏渲染的Link中的介绍，
也可以看另一位大神ibireme对渲染流畅的文章，[iOS 保持界面流畅的技巧](http://blog.ibireme.com/2015/11/12/smooth_user_interfaces_for_ios/)

简单的说就是`CALayer`的`圆角`和`阴影`，当出现在大量的cell之中，会进项很多的离屏渲染，这样就会大幅度拖慢FPS

如何解决？
>圆角使用UIImageView来处理。
简单来说，底层铺一个UIImageView,然后用GraphicsContext生成一张带圆角的图。

####11) App沙盒数据存储目录

[一些代码建议](http://www.reviewcode.cn/article.html?reviewId=8)

>数据存储应该再谨慎一些，至少用户数据可以放在 Documents 文件夹下某个子目录里，而不应该直接丢到 Documents 文件夹下，清空时也不应该清空整个 Documents 文件夹。

PS:顺带我想说，如果app配置了itunes查看Documents的功能，apple审核的时候会查看documents目录，一些非用户可感知的数据，程序生成的数据，存放在Doc目录下，可能会被苹果拒审

####12） 即时抽取函数

[话谈 iOS 目录结构的划分](http://www.reviewcode.cn/article.html?reviewId=9)

可以细看Link中的案例

简单描述就是，随着业务的不断增长，有时候会出现超长的函数，有时候会有相似代码，被写出来，适当的即时抽取函数，减少超长代码，减少近似冗余代码

####13） 使用懒加载
[好的代码习惯](http://www.reviewcode.cn/article.html?reviewId=10)

 	[self initComps];
    [self initToolbar];
    [self initVertical];
    [self initImageView];
    [self initMediaPick];
    [self setupSpeechRecognizer];
    [self initAttributedString];
    [self initTextView];

这样的代码，推荐使用懒加载

>懒加载带来的收益：我们不再需要显式的生成和调用initAttributedString方法，只需要在使用的时候调用属性self.attrString，对象的实例化全部放在getter中，可以有效降低代码的耦合度;在使用属性之前，属性并不会提前生成，减少内存占用。

####13）delegate校验参数
[好的代码习惯](http://www.reviewcode.cn/article.html?reviewId=10)

	- (void)textViewDidEndEditing:(YYTextView *)textView {
	    if (textView == self.textView) {
	        self.navigationItem.rightBarButtonItem = nil;
	    }
	}
	
>如果你的delegate方法，只作为一个textView的委托回调，这种写法没有任何。但是如果你想扩展你的界面，在将来的界面中很可能出现另一个textView，这时你就必须区分这两个textView是谁回调了这个代理方法

###四. 项目配置

####1）目录结构
[话谈iOS目录结构的划分](http://www.reviewcode.cn/article.html?reviewId=9)

提到了MVC结构，以及MVC结构下如何划分目录结构

>往往业界有两种做法：

>先按业务划分，再按照 MVC 来划分

>先按 MVC 划分，再按照业务划分

>第一种的好处是把相应业务的代码放在一起，找特别好找，相应的 xib、model 和 ViewController 全在一个地方。在这些代码之间跳转特别方便。Telegram 非常大的代码量，也是这么组织的。个人觉得如果代码量特别大，这种划分方式其实更好，先按照业务划分了，更容易分工合作。

>第二种似乎更多人用。Yep 也是按照这样的方式组织。

>其实我觉得都可以，看个人习惯。

PS:我表示，我可能更习惯`先按业务模块划分，再MVC`

####2）合理高效的开发环境
[如何打造令人愉悦的开发环境](http://www.reviewcode.cn/article.html?reviewId=1)

这个案例里面详尽探讨了一个观点 `一个合理高效的开发环境应该是依托于自动化之上的.`

自动化应当包含以下几个方面:
- 代码风格检查
- 自动化测试
- 持续集成
- 常用库的封装和打包

####3）第三方库管理
[如何打造令人愉悦的开发环境](http://www.reviewcode.cn/article.html?reviewId=1)
[要你命三千：老代码中的那些坑](http://www.reviewcode.cn/article.html?reviewId=3)

- 各种第三方库推荐使用cocoapods管理，提高效率
- 项目勤用三方库，随意穿插改无数。 即使类库有更新，试问代码谁维护


###持续更新
codeReview应该持续进行下去，这个总结也应该持续进行。

扔到Git上吧，[iOSCodeReviewTipsCollection](https://github.com/Awhisper/iOSCodeReviewTipsCollection)，（╮(╯_╰)╭ 又TM是广告)