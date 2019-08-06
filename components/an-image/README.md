### AnImage 蚁点（Andot）媒体图片组件 使用说明

> Introducation 介绍

为什么要做这个插件呢，官网已经有<imgae></image>标签了？
因为太烂了，不符合业务需求呀，如果一个列表，并且列表中如果没有图片，
找一个默认图片，你有什么办法吗，反正我是木有了，可能需求也比较特殊吧！
如果你有，请在评论中说出来，感谢您！

> 这个就是符合我们HTML中的写法

> 废话不多说，马上使用

> 引入组件：

```
import anImage from '@/components/an-image/an-image'

export default {
	components:{
		anImage
	},
}
```

> 使用组件

```
<an-image :src="'https://andot.org/'+name+'.jpg'" alt="https://andot.org/images/default.png"></an-image>
```

> 属性

属性名 | 类型 | 默认值 | 说明 | 平台差异说明 
-|-|-
src | String | '' | 图片地址 | 无
alt | String | '' | 如果图片无法加载，则默认显示图片地址 | 无
mode | String | 'scaleToFill' | 图片裁剪、缩放的模式 | 无
width | Number | 70 | 图片宽度，单位：小于1( 0.2 => 20% )则为百分比，大于1( 20=>20px )为px | 无
height | Number | 90 | 图片高度，单位：小于1( 0.2 => 20% )则为百分比，大于1( 20=>20px )为px | 无

> mode 属性具体详细请看官网
[mode 有效值](https://uniapp.dcloud.io/component/image)

### 1.1 Update log

> 解决了当数据重新加载，导致图片不切换bug

> 有大家可能问我为什么，我的标签前面都有一个an， 因为工作室为Andot Studio， 所以使用an， 蚁点（Andot）
网站：https://andot.org