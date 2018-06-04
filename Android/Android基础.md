### 控件

ExpandableListView + 实现BaseExpandableListAdapter的Adapter 实现 社交应用的评论和回复功能。[相关网站](https://www.jianshu.com/p/eda8d09c9d7a)


### 官方适配方案
在Galaxy S8发布之后，Android官方提供了适配方案，即提高App所支持的最大屏幕纵横比，实现很简单，在AndroidManifest.xml中可做如下配置：

<meta-data android:name="android.max_aspect"
    android:value="ratio_float"/>
1
2
其中ratio_float为浮点数，官方建议为2.1或更大，因为18.5：9=2.055555555……，如果日后出现纵横比更大的手机，此值将会更大。

另外如果没有上述设置，android:resizeableActivity 也为false的话，则应用所支持的最大纵横比为默认值1.86，即默认无法支持全面屏。

