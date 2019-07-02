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
	<text>Hello Andot</text>
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