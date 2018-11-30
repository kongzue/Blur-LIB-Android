# Blur-LIB-Android(zh-cn)

模糊视图背景库（中文文档）.

[<img src="/Artwork/PhoneAndScreen.gif" width="400"/>](https://youtu.be/sYPqS0px61Q)

[在youtube上查看范例](https://youtu.be/sYPqS0px61Q)

## 工作原理
采用硬件加速原理，模糊变得非常快。使用Surface.LockhardWareCanvas()将要模糊的背景视图渲染成表面纹理。
然后使用高斯模糊算法模糊表面纹理，并使用OpenGL在表面视图或纹理视图中渲染。

## 下载使用
Gradle 方式：
```
   implementation 'no.danielzeller.blurbehindlib:blurbehindlib:1.0.0'
```
或者使用 Maven 方式：
```
   <dependency>
     <groupId>no.danielzeller.blurbehindlib</groupId>
     <artifactId>blurbehindlib</artifactId>
     <version>1.0.0</version>
     <type>pom</type>
   </dependency>
```

## 基础
在布局文件中使用BlurBehindLayout：

```xml
    <no.danielzeller.blurbehindlib.BlurBehindLayout
        android:id="@+id/blurBehindLayout"
        android:layout_width="match_parent"
        android:layout_height="50dp"
       
        app:blurRadius="100.0" 
        app:updateMode="onScroll"
        app:useTextureView="false"
        app:blurPaddingVertical="50dp"
        app:blurTextureScale="0.5"
        app:useChildAlphaAsMask="false">
        <!-- 子布局 -->
        </no.danielzeller.blurbehindlib.BlurBehindLayout>
```

然后，您需要设置BlueBehindLayout后面的视图(将会模糊的视图)

```kotlin
     blurBehindLayout.viewBehind = viewToBlur
```

[<img src="/Artwork/Transition.gif" width="400"/>](https://youtu.be/sYPqS0px61Q)

#### 模糊半径
<table>
  <tr>
    <td width="50%"><div class="highlight"><pre>app:blurRadius = "100.0"</pre></div></td>
    <td width="50%"><div class="highlight"><pre>blurBehindLayout.blurRadius = 100.f</pre></div></td>
  </tr>
</table>
确定模糊程度。应该是介于0f - 200f之间的浮点值，默认值为40f。

#### 更新模式
<table>
  <tr>
    <td width="50%"><div class="highlight"><pre>app:updateMode = "continuously"</pre></div></td>
    <td width="50%"><div class="highlight"><pre>blurBehindLayout.updateMode = UpdateMode.CONTINUOUSLY</pre></div></td>
  </tr>
</table>
确定如何更新BlueBehindLayout。当更新模式为UpdateMode.CONTINUOUSLY时。不断重复调用渲染器来重新渲染场景。
当更新模式为UpdateMode.ON_SCROLL时，渲染器仅在视图滚动时渲染。
当更新模式为UpdateMode.MANUALLY时。手动渲染器仅在创建表面和UpdateFormalisSeconds(..)是手动调用的。这在制作背景动画或过渡过程中非常有用。


#### 使用纹理视图
```
    app:useTextureView = "true"
```
这只能在BlueBehindLayout的构造函数中从XML或使用代码中的常规构造函数进行更改。默认值为false。只有当SurfaceView不是一个选项时，才应该使用纹理视图，因为Z排序中断，或者如果你激活了BlueBehindLayout的Alpha值。使用纹理视图代替表面视图对性能影响很小。

#### 模糊纹理比例
```
    app:blurTextureScale = "0.5"
```
应该是介于0.1f - 1f之间的值。建议至少向下采样到0.5f。该比例对性能有很大影响，所以尽量保持低水平。默认值为0.4f。这只能在BlueBehindLayout的构造函数中从XML或使用代码中的常规构造函数来设置。


#### 垂直填充
```
    app:blurPaddingVertical = "50dp"
```
你可以用这个使模糊纹理在垂直方向上大于模糊纹理。例如，当背景视图向上和向下滚动时，使用填充会看起来更好，因为它减少了新像素进入模糊区域时的闪烁。


#### 使用子布局alpha遮罩
```
    app:useChildAlphaAsMask = "true"
```
如果这是真的，则将BlurBehindLayout的第一个子视图渲染到纹理中。 然后将该纹理的alpha值用作Blur纹理的遮罩。 当useChildAlphaAsMask为true时，useTextureView也将被强制为true以支持透明度。
此效果可用于创建背景模糊的文本等。 有关示例，请参阅DialogFragment。


## 联系

你可以访问Twitter： [@zellah](https://twitter.com/zellah) or [email](mailto:hello@danielzeller.no).


## 开发者

由 Daniel Zeller 开发 - [danielzeller.no](http://danielzeller.no/), 一个位于挪威奥斯陆的自由开发者。

翻译为中文： [kongzue](https://github.com/kongzue)

