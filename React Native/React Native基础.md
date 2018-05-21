
[组件生命周期](https://www.race604.com/react-native-component-lifecycle/)

![生命周期图](http://7rf9ir.com1.z0.glb.clouddn.com/3-3-component-lifecycle.jpg)




'Navigator is deprecated and has been removed from this package. It can now be installed '

这是因为版本升级到0.43以上的话，Navigator不能直接从react-native里面获取了，npm install react-native-deprecated-custom-components --save
然后在引用的地方 import {Navigator} from react-native-deprecated-custom-components

