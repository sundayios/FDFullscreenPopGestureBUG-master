解决FDFullscreenPopGesture连续多个页面隐藏导航栏的BUG
96  _moses 关注
2018.01.02 23:18* 字数 413 阅读 148评论 0喜欢 0
下面的方法可以用FDFullscreenPopGesture实现相邻页面的导航栏任意交替隐藏和显示(主要解决连续多个页面隐藏导航栏出现的BUG)

实现方法：

在所有需要隐藏导航栏的页面加上如下代码
@property (nonatomic, assign) BOOL previousNaviBarShow;
#import "UINavigationController+FDFullscreenPopGesture.h"

- (void)viewWillAppear:(BOOL)animated {
[super viewWillAppear:animated];
// 在所有需要隐藏导航栏的页面加上这两行代码，所有需要显示导航栏的页面不做任何操作即可
self.fd_prefersNavigationBarHidden = YES;
[self.navigationController setNavigationBarHidden:YES animated:self.previousNaviBarShow];
}
在所有 由(显示导航栏页面)推出(隐藏导航栏页面)的地方，把要推出页面的previousNaviBarShow置为YES
