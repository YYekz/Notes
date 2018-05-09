### 动态变量
有时，特定的绑定类是未知的。例如，RecyclerView.Adapter针对任意布局的操作不知道特定的绑定类。它仍然必须在调用onBindViewHolder()方法期间分配绑定值。

在以下示例中，所有RecyclerView绑定具有 item变量的布局。该BindingHolder对象有一个getBinding()返回ViewDataBinding基类的方法 。

public void onBindViewHolder(BindingHolder holder, int position) {
  final T item = mItems.get(position);
  holder.getBinding().setVariable(BR.item, item);
  holder.getBinding().executePendingBindings();
}


### Observable观察数据和LiveData对比
