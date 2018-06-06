### 控件

ExpandableListView + 实现BaseExpandableListAdapter的Adapter 实现 社交应用的评论和回复功能。[相关网站](https://www.jianshu.com/p/eda8d09c9d7a)


### 官方适配方案
在Galaxy S8发布之后，Android官方提供了适配方案，即提高App所支持的最大屏幕纵横比，实现很简单，在AndroidManifest.xml中可做如下配置：

```
<meta-data android:name="android.max_aspect"
    android:value="ratio_float"/>
```

其中ratio_float为浮点数，官方建议为2.1或更大，因为18.5：9=2.055555555……，如果日后出现纵横比更大的手机，此值将会更大。

另外如果没有上述设置，android:resizeableActivity 也为false的话，则应用所支持的最大纵横比为默认值1.86，即默认无法支持全面屏。


### 事件分发机制

 onTouchListener > onTouchEvent > onLongClickListener > onClickListener
 
 安卓为了保证所有的事件都是被一个 View 消费的，对第一次的事件( ACTION_DOWN )进行了特殊判断，View 只有消费了 ACTION_DOWN 事件，才能接收到后续的事件(可点击控件会默认消费所有事件)，并且会将后续所有事件传递过来，不会再传递给其他 View，除非上层 View 进行了拦截。

#### 核心要点
1. 事件分发原理: 责任链模式，事件层层传递，直到被消费。
2. View 的 dispatchTouchEvent 主要用于调度自身的监听器和 onTouchEvent。
3. View的事件的调度顺序是 onTouchListener > onTouchEvent > onLongClickListener > onClickListener 。
4. 不论 View 自身是否注册点击事件，只要 View 是可点击的就会消费事件。
5. 事件是否被消费由返回值决定，true 表示消费，false 表示不消费，与是否使用了事件无关。
6. ViewGroup 中可能有多个 ChildView 时，将事件分配给包含点击位置的 ChildView。
7. ViewGroup 和 ChildView 同时注册了事件监听器(onClick等)，由 ChildView 消费。
8. 一次触摸流程中产生事件应被同一 View 消费，全部接收或者全部拒绝。
9. 只要接受 ACTION_DOWN 就意味着接受所有的事件，拒绝 ACTION_DOWN 则不会收到后续内容。
10. 如果当前正在处理的事件被上层 View 拦截，会收到一个 ACTION_CANCEL，后续事件不会再传递过来。


