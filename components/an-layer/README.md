锘�### AnLayer 浣跨敤璇存槑

> 寮曞叆缁勪欢锛�

```
import anLayer from '@/components/an-layer/an-layer'

export default {
	components:{
		anLayer
	},
}
```

> 浣跨敤缁勪欢

```
<an-layer ref="anRef" autoClose="true" timer="3" type="info">
	<text>Hello Andot</text> <!-- 鍙互瀹氫箟鍙橀噺锛岃繖涓篃鏄簾璇濓紝閮界煡閬搟{message}} -->
</an-layer>

//寮�鍚� 濡傛灉璁剧疆浜哸utoClose 鍒欒嚜鍔ㄥ叧闂�
this.$refs.anRef.show();
//鍏抽棴
this.$refs.anRef.close();
```

> 灞炴��

灞炴�у悕 | 绫诲瀷 | 榛樿鍊� | 璇存槑 | 骞冲彴宸紓璇存槑 
-|-|-
<<<<<<< HEAD
showPop | Boolean | false | 鏄惁鏄剧ず閬洊灞� | 鏃�
direction | String | "top" | 寮瑰嚭鏂瑰悜 | 鏃�
autoClose | Boolean | true | 鏄惁鑷姩鍏抽棴灞� | 鏃�
time | Number | 2 | 鑷姩鍏抽棴鍊掕鏃剁鏁帮紝榛樿2绉� | 鏃�
type | String | 'info' | 寮圭獥绫诲瀷瀵瑰簲涓嶅悓棰滆壊锛坕nfo銆乻uccess銆� warn銆乪rror锛墊 鏃�
=======
showPop | Boolean | false | 是否显示遮盖层 | 无
direction | String | "top" | 弹出方向 | 无
autoClose | Boolean | true | 是否自动关闭层 | 无
timer | Number | 2 | 自动关闭倒计时秒数，默认2秒 | 无
type | String | 'info' | 弹窗类型对应不同颜色（info、success、 warn、error）| 无
>>>>>>> 5df3e2602a390e255c6472bd8c311bb7b362d277

### 1.1 鏇存柊鐗堟湰璇存槑

#### 鏂板show鏂规硶鐩存帴浼犺緭鎻愮ず娑堟伅鍙傛暟

> 鍙傛暟

鍙傛暟 | 绫诲瀷 | 榛樿鍊� | 璇存槑 | 骞冲彴宸紓璇存槑 
-|-|-
message | String | false | 鍦╯how()閲岄潰鐩存帴浼犲叆锛屼紭鍏堢骇楂橈紝濡傛灉鏍囩涔熸湁锛宻how锛堬級涔熸湁鍙傛暟锛屾樉绀簊how()閲岄潰鐨勬秷鎭� | 鏃�

> 浣跨敤鏂规硶

```
<an-layer ref="anRef" autoClose="true" timer="3" :type="type">
	<text>Hello Andot</text>   <!-- 鍐欎簡show鍙傛暟灏变笉瑕佸啓杩欓噷浜嗭紝杩欎釜鍦版柟鍐欎笉鍐欙紝涔熷�掓槸鏃犳墍璋擄紝濡傛灉浣犳槸寮鸿揩鐥囷紝鍐欎笂涔熸病浜嬶紝鍙嶆涓嶄細鏄剧ず-->
</an-layer>

//寮�鍚� 濡傛灉璁剧疆浜哸utoClose 鍒欒嚜鍔ㄥ叧闂�
this.$refs.anRef.show(鈥�'Hello Lucas');
//鍏抽棴
this.$refs.anRef.close();

//鏈�缁堟樉绀烘晥鏋滀负 Hello Lucas 
```

#### 1.2鏇存柊鐗堟湰璇存槑

> 澧炲姞寮瑰嚭鍔ㄧ敾锛岀紦鎱笅钀藉姩鐢�

#### 1.3锛�2019-07-03锛�

> 鍔ㄧ敾-鍜宻how閲岄潰娣诲姞鍙傛暟鏁村悎 1.1鐗堟湰鍜�1.2鐗堟湰鐨勪竴涓暣鍚堢増锛屾帹鑽愪娇鐢�

#### 1.4锛�2019-07-04锛�

> 淇浠庝笅鍜屽彸鏂瑰悜寮瑰嚭鍑虹幇鐨刡ug 缇庡寲鐣岄潰

#### 1.5锛�2019-07-05锛�

<<<<<<< HEAD
> 1銆佷慨澶嶈嫢骞瞓ug
> 2銆佸鍔犲乏渚с�佸彸渚у脊绐楃殑鏍囬
> 3銆佸鍔犲乏渚с�佸彸渚у脊绐楃殑鍐呭瓒呭嚭鍙互杩涜婊氬姩

### 1.6 (2019-7-11)

> show() 鏂规硶涓師鏉ュ鍔犱簡涓�涓秷鎭弬鏁帮紝鐜板湪澧炲姞涓�涓猳ption鍙傛暟锛� 涓轰簡澶у鏂逛究璋冪敤

> 鍔犺繖涓弬鏁版槸鐩存帴鍙互锛屾坊鍔犱竴涓爣绛撅紝鍙互澶氱鍦烘櫙璋冪敤

> 渚嬪璇达紝澶辫触鎴戠敤type涓篹rror锛屾垚鍔熷垯鐢╰ype涓簊uccess鐨勶紝杩欐牱灏变笉闇�瑕佸啓澶氫釜鏍囩浜�

### 1.7 (2019-7-31)

> 瀵笻5鏍峰紡鍋氬吋瀹瑰鐞�


#### 鐩存帴杩欐牱涔﹀啓锛堬級

```
this.$refs.anRef.show("鎴愬姛鍟︼紒", {
	type: 'success'
});
this.$refs.anRef.show("浣犲け璐ヤ簡锛屼綘瑙夊緱搴旇鍚楋紵", {
=======
> 1、修复若干bug
> 2、增加左侧、右侧弹窗的标题
> 3、增加左侧、右侧弹窗的内容超出可以进行滚动

### 1.6 (2019-7-11)

> show() 方法中原来增加了一个消息参数，现在增加一个option参数， 为了大家方便调用

> 加这个参数是直接可以，添加一个标签，可以多种场景调用

> 例如说，失败我用type为error，成功则用type为success的，这样就不需要写多个标签了

#### 直接这样书写（）

```
this.$refs.anRef.show("成功啦！", {
	type: 'success'
});
this.$refs.anRef.show("你失败了，你觉得应该吗？", {
>>>>>>> 5df3e2602a390e255c6472bd8c311bb7b362d277
	type: 'error'
});
```

<<<<<<< HEAD
#### option 鏄竴涓璞★紝閲岄潰鏈変互涓嬪嚑涓弬鏁�
灞炴�у悕 | 绫诲瀷 | 榛樿鍊� | 璇存槑
-|-|-
showPop | Boolean | false | 鏄惁鏄剧ず閬洊灞�
direction | String | "top" | 寮瑰嚭鏂瑰悜
autoClose | Boolean | true | 鏄惁鑷姩鍏抽棴灞�
timer | Number | 2 | 鑷姩鍏抽棴鍊掕鏃剁鏁�
type | String | 'info' | 寮圭獥绫诲瀷瀵瑰簲涓嶅悓棰滆壊锛坕nfo銆乻uccess銆� warn銆乪rror锛�
=======
#### option 是一个对象，里面有以下几个参数
属性名 | 类型 | 默认值 | 说明
-|-|-
showPop | Boolean | false | 是否显示遮盖层
direction | String | "top" | 弹出方向
autoClose | Boolean | true | 是否自动关闭层
timer | Number | 2 | 自动关闭倒计时秒数
type | String | 'info' | 弹窗类型对应不同颜色（info、success、 warn、error）
>>>>>>> 5df3e2602a390e255c6472bd8c311bb7b362d277
