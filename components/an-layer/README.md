### AnLayer 使用说明

> 引入组件：

```
import anLayer from '@/components/an-layer/an-layer'

export default {
	components:{
		anLayer
	},
}
```

> 使用组件

```
<an-layer ref="anRef" autoClose="true" timer="3" type="info">
	<text>Hello Andot</text> <!-- 可以定义变量，这个也是废话，都知道{{message}} -->
</an-layer>

//开启 如果设置了autoClose 则自动关闭
this.$refs.anRef.show();
//关闭
this.$refs.anRef.close();
```

> 属性

属性名 | 类型 | 默认值 | 说明 | 平台差异说明 
-|-|-
showPop | Boolean | false | 是否显示遮盖层 | 无
direction | String | "top" | 弹出方向 | 无
autoClose | Boolean | true | 是否自动关闭层 | 无
timer | Number | 2 | 自动关闭倒计时秒数，默认2秒 | 无
type | String | false | 弹窗类型对应不同颜色（info、success、 warn、error）| 无

### 1.1 更新版本说明

#### 新增show方法直接传输提示消息参数

> 参数

参数 | 类型 | 默认值 | 说明 | 平台差异说明 
-|-|-
message | String | false | 在show()里面直接传入，优先级高，如果标签也有，show（）也有参数，显示show()里面的消息 | 无

> 使用方法

```
<an-layer ref="anRef" autoClose="true" timer="3" :type="type">
	<text>Hello Andot</text>   <!-- 写了show参数就不要写这里了，这个地方写不写，也倒是无所谓，如果你是强迫症，写上也没事，反正不会显示-->
</an-layer>

//开启 如果设置了autoClose 则自动关闭
this.$refs.anRef.show(‘'Hello Lucas');
//关闭
this.$refs.anRef.close();

//最终显示效果为 Hello Lucas 
```

#### 1.2更新版本说明

> 增加弹出动画，缓慢下落动画

#### 1.3（2019-07-03）

> 动画-和show里面添加参数整合 1.1版本和1.2版本的一个整合版，推荐使用

#### 1.4（2019-07-04）

> 修复从下和右方向弹出出现的bug 美化界面

#### 1.5（2019-07-05）

> 1、修复若干bug
> 2、增加左侧、右侧弹窗的标题
> 3、增加左侧、右侧弹窗的内容超出可以进行滚动