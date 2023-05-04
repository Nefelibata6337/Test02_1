# Test02_1
# Android Studio构建第一个Kotlin应用
![在这里插入图片描述](https://img-blog.csdnimg.cn/7dff7dde627f4dd8afbc96d56fbf2b51.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/5ac96a19d3974e50a6baffae57836df0.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/bc0ec79823df46e49dec20d627788ecc.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/b9cc93ad8b8146a6bf2297b04431d88c.png#pic_center)
### 参考：
[Android Studio报：Connection timed out: connect. If you are behind an HTTP proxy错误](https://blog.csdn.net/Ryanymk/article/details/116542100)
![在这里插入图片描述](https://img-blog.csdnimg.cn/ca8690814560441baf1aeab6d517d484.png#pic_center)

## 探索界面布局编辑器

 - 每个界面由一个Fragment组成，初始界面显示的FirstFragment，双击fragment_first.xml可以查看具体的布局设计界面。

 res——>layout——f>ragment_first.xml
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/e39c23b0c4d74287a37059f8c0047da7.png#pic_center)

 1. Palette：包含您可以拖到布局中的各种视图和视图组。 
 2. Component Tree：显示布局中的组件层次结构。   
 3. 工具栏：点击这些按钮可在编辑器中配置布局外观及更改布局属性。 
 4. 设计编辑器：在 Design 视图和/或 Blueprint视图中修改布局。 
 5. Attributes：用于对所选视图的属性进行控制的控件。 
 6. 视图模式：采用 Code 模式图标、Design 模式图标 或 Split 模式图标 模式查看布局。Split 模式会同时显示 Code 和 Design 窗口。
 7. 缩放和平移控件：控制编辑器内的预览大小和位置。

当您打开 XML 布局文件时，系统会默认打开设计编辑器，如图 1 所示。如需在文本编辑器中修改布局 XML，请点击窗口右上角的 Code 模式图标 按钮。请注意，在 Code 视图中修改布局时，Palette、Component Tree 和 Attributes 窗口不可用。

> 提示：您只需按 Alt + Shift + Right/Left arrow（在 Mac 上按 Control + Shift + Right/Left arrow），即可在设计编辑器和文本编辑器之间切换。

详细看[使用布局编辑器构建界面](https://developer.android.google.cn/studio/write/layout-editor?hl=zh-cn)
### 查看code，修改Textview的Text属性
```
android:text="@string/hello_first_fragment"
```

右键该代码，选择Go To > Declaration or Usages，跳转到values/strings.xml，看到高亮文本

```
<string name="hello_first_fragment">Hello first fragment</string>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/f915acad256d411fa94f63e5905312f4.png#pic_center)
注意，不要全选一行，全选会跳转至attrs.xml文件

修改字符串属性值为“Hello Kotlin!”。更进一步，修改字体显示属性，在Design视图中选择
textview_first文本组件，在Common Attributes属性下的textAppearance域，设置相关的文字显示属性。
![在这里插入图片描述](https://img-blog.csdnimg.cn/4eb47d8d2ddf42969f9bc2e04034bafb.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/fa868b7edc1d492aac4d83451afe9025.png#pic_center)
重新运行应用程序，查看显示效果。
### 向页面添加更多的布局
本步骤将向第一个Fragment添加更多的视图组件
#### 查看视图的布局约束
在fragment_first.xml，查看TextView组件的约束属性：
![在这里插入图片描述](https://img-blog.csdnimg.cn/26ae9a38fb9e4fb69b79379d8d3fc0f5.png#pic_center)
详细查看[使用 ConstraintLayout 构建自适应界面](https://developer.android.google.cn/training/constraint-layout?hl=zh-cn)

#### 添加按钮和约束
从Palette面板中拖动Button到
![在这里插入图片描述](https://img-blog.csdnimg.cn/e42fef70d5a04d4db1352b42b80369a5.png#pic_center)
调整Button的约束，设置Button的Top>BottonOf textView
```
app:layout_constraintTop_toBottomOf="@+id/textview_first" />
```
约束条件可以是
```
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
```
也可以是
```
		tools:ignore="MissingConstraints"
```
调整Next按钮
Next按钮是工程创建时默认的按钮，查看Next按钮的布局设计视图，它与TextView之间的连接不是锯齿状的而是波浪状的，表明两者之间存在链（chain），是一种两个组件之间的双向联系而不是单向联系。删除两者之间的链，可以在设计视图右键相应约束，选择Delete（注意两个组件要双向删除）
![在这里插入图片描述](https://img-blog.csdnimg.cn/a71a041b4d7b4ec78ade2baaef6fe487.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/101e41bbff894472ad44502149fca5ed.png#pic_center)
或者在属性面板的Constraint Widget中移动光标到相应约束点击删除。
![在这里插入图片描述](https://img-blog.csdnimg.cn/c2437b6fbf984f97bd78cd15aa25e0cc.png#pic_center)
同时，删除Next按钮的左侧约束。

#### 添加新的约束
添加Next的右边和底部约束至父类屏幕（如果不存在的话），Next的Top约束至TextView的底部。最后，TextView的底部约束至屏幕的底部。效果看起来如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/b8fb42a661df4c9da41cc8ea0095d9ca.png#pic_center)
#### 更改组件的文本
fragment_first.xml布局文件代码中，找到toast_button按钮的text属性部分
>       android:id="@+id/toast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="450dp"
        android:insetBottom="0dp"
        android:text="Button"

这里text的赋值是一种硬编码，点击文本，左侧出现灯泡状的提示，选择 Extract string resource。
![在这里插入图片描述](https://img-blog.csdnimg.cn/a945a60671094c05b5865e2cc726aff0.png#pic_center)
弹出对话框，令资源名为toast_button_text，资源值为Toast，并点击OK。
![在这里插入图片描述](https://img-blog.csdnimg.cn/27693ed24fca4134be7f6adf3f182966.png#pic_center)
于是，在资源文件string.xml定义了字符串，以上操作可以手动在string.xml文件中定义并引用。

```
<resources>
   ... 
   <string name="toast_button_text">Toast</string>
</resources>
```
#### 更新Next按钮
在属性面板中更改Next按钮的id，从button_first改为random_button。
![在这里插入图片描述](https://img-blog.csdnimg.cn/29389d6ae2fb4f73b494d268a39d1a2f.png#pic_center)
在**string.xml**文件，右键**next**字符串资源，选择 **Refactor > Rename**，修改资源名称为**random_button_text**，点击**Refactor** 。随后，修改**Next**值为**Random**。
![在这里插入图片描述](https://img-blog.csdnimg.cn/fa941d70ba7c454aa664955bb9624177.png#pic_center)
#### 添加第三个按钮
向fragment_first.xml文件中添加第三个按钮，位于Toast和Random按钮之间，TextView的下方。新Button的左右约束分别约束至Toast和Random，Top约束至TextView的底部，Buttom约束至屏幕的底部，看起来的效果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/1e08dd070a924fefbc2d6ddb0d66d2c3.png#pic_center)
检查xml代码，确保不出现类似app:layout_constraintVertical_bias这样的属性，即不手动设置偏移量。
完善UI组件的属性设置
更改新增按钮id为count_button，显示字符串为Count，对应字符串资源值为count_button_text。于是三个按钮的text和id属性如下表：
|Button| Text | Id |
|--|--|--|
| LeftButton | Toast | @+id/toast_button |
|--|--|--|
| MiddleButton | Count | @+id/count_button |
|--|--|--|
| RightButton | Random | @+id/random_button |
同时，更改TextView的文本为0。修改后的fragment_first.xml的代码

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".FirstFragment">

    <TextView
        android:id="@+id/textview_first"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="sans-serif-thin"
        android:text="@string/hello_first_fragment"
        android:textSize="20sp"
        app:layout_constraintBottom_toTopOf="@id/random_button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />


    <Button
        android:id="@+id/random_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="250dp"
        android:text="@string/random_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/toast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="250dp"
        android:insetBottom="0dp"
        android:text="@string/toast_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/count_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/count_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/random_button"
        app:layout_constraintStart_toEndOf="@+id/toast_button"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
### 尝试运行应用程序查看效果。
#### 更新按钮和文本框的外观
添加新的颜色资源
values>colors.xml定义了一些应用程序可以使用的颜色，添加新颜色screenBackground 值为 #2196F3，这是蓝色阴影色；添加新颜色buttonBackground 值为 #BBDEFB

```kotlin
<color name="screenBackground">#2196F3</color>
<color name="buttonBackground">#BBDEFB</color>
```
#### 设置组件的外观
1. fragment_first.xml的属性面板中设置屏幕背景色为

```kotlin
android:background="@color/screenBackground"
```
2. 设置每个按钮的背景色为buttonBackground

```kotlin
android:background="@color/buttonBackground"
```
**注意**：在实验的API level中（31），这种设置并不生效，需修改res/values/themes.xml的style值，添加```.Bridge```。

```kotlin
<style name="Theme.MyFirstApp" parent="Theme.MaterialComponents.DayNight.DarkActionBar.Bridge">
```
3. 移除TextView的背景颜色，设置TextView的文本颜色为color/white，并增大字体大小至72sp。
### 设置组件的位置
1. Toast与屏幕的左边距设置为24dp，Random与屏幕的右边距设置为24dp，利用属性面板的Constraint Widget完成设置。
2. 设置TextView的垂直偏移为0.3。

```kotlin
app:layout_constraintVertical_bias="0.3"
```
拖动左侧的移动条。
![在这里插入图片描述](https://img-blog.csdnimg.cn/8eb33c78228740c080ee20fc1a4a15da.png#pic_center)
### 最终代码

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".FirstFragment"
    android:background="@color/screenBackground">

    <TextView
        android:id="@+id/textview_first"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="sans-serif-thin"
        android:text="@string/hello_first_fragment"
        android:textSize="72sp"
        app:layout_constraintBottom_toTopOf="@id/random_button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:background="@color/white"/>


    <Button
        android:id="@+id/random_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="700dp"
        android:layout_marginEnd="24dp"
        android:text="@string/random_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:background="@color/buttonBackground"
        />

    <Button
        android:id="@+id/toast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginTop="700dp"
        android:insetBottom="0dp"
        android:text="@string/toast_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:background="@color/buttonBackground"
        />

    <Button
        android:id="@+id/count_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="-290dp"
        android:background="@color/buttonBackground"
        android:text="@string/count_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/random_button"
        app:layout_constraintHorizontal_bias="0.542"
        app:layout_constraintStart_toEndOf="@+id/toast_button"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
