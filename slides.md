---
theme: seriph
# background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Welcome to Slidev
mdc: true
---

# Jetpack Compose Introduction

Zech & Harry

- What is Jetpack Compose?
- The difference between Compose and our current UI development?
- The Advantage and Disadvantage of Compoe

---
transition: fade-out
---

# 什么是 Jetpack Compose?

Jetpack Compose 是 Google 推出的一种新型的写 UI 的编程范式

- **📝 简洁** - 更简洁的语法糖，更高效的编写 UI
- **🛠 声明式** - 更加现代易懂 UI 编程范式，大家都在用
- **🧩 组件化** - 使用可重用的组件构成，可以快速搭建较为复杂的 UI
- **👀 可预览** - 可以在编辑器里实时预览 UI 变化

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Compose 的优缺点

## 简洁

这是以前写列表的方法：
```xml {5-8}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rv"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
```

``` kotlin
class ItemAdapter: RecyclerView.Adapter<ViewHolder>() {
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
    }
    override fun getItemCount(): Int {
    }
    override fun onBindViewHolder(holder: ViewHolder, position: Int) {
    }
}
```

<!-- 
我们来了解一下 Compose 的优缺点，第一个最显而易见的区别就是简洁，可以使用更简单的语法来实现 native UI，而不是 flutter 那种自己实现的 UI 框架，不会有性能损失。简洁带来的另一个作用就是开发效率会提升。

以列表为例，如果在以前我们想写一个竖向的列表，我们需要写很多类和文件
先在 xml 里写 RecyclerView 的样式，然后还要定义 Adapter，在 Adapter 里还要定义每一个 Item 的样式，然后还得将数据传入 adapter 以及 item，最后还要定义 RecyclerView 的 LayoutManager 确定更加细节的样式。这里只展示了一点点，大家都写过知道有多麻烦。
-->

---

这是使用 Compose 写列表的方法

```kotlin {1|2|3-7|4-6|all}
@Composable
fun ItemList(data: List<String>) {
    LazyColumn {
        items(data) { name ->
            Text(text = name)
        }
    }
}
```

<!-- 
这里大家先不用深入，后面 Zech 会详细讲解 Compose 的语法

简单的说这里的 @Compose 代表了这个方法是一个 Compose 的 View  [点击]

它的传入参数是一个字符串列表，代表了它要显示的数据 [点击]

LazyColumn 就是和 RecyclerView 类似的一个竖向列表 [点击]

里面的 items 是 compose 的一个语法，将你要展示的数据传进来，然后在回调里就可以调用列表里的数据了。 [点击]

最后这个 Text 就是我们要展示的 ItemView [点击]

这样只用了 8 行就写好了一个简单的列表，这就是 Compose 的第一个优点，简洁
-->
---
layout: image-right

image: https://i.imgur.com/kZMD4ZT.png
---

## 可预览

使用 Jetpack Compoe 可以直接在右边预览每个页面，甚至是每个组件

而且是实时预览

## 和原来的代码可以一起使用

原有项目也可以直接使用 Jetpack Compose

<!-- 
使用 Jetpack Compoe 可以直接在右边预览每个页面，甚至是每个组件

而且是实时预览

可以看到右图是我们的 debug menu 快速跳转的 app，大家先忽略很丑的 UI，可以看到整个页面组件的预览，也可以看到单个按钮的预览

那我们来看一下实时预览吧[跳转到 demo]
-->

---

## 声明式

声明式编程是一种比较新的编程方式，至少在 UI 上是这样

### 有哪些 UI 开发用到了声明式？

#### React
```jsx
function MyComponent(props) {

  const { items } = props;

  return (
    <ul>
      {items.map(item => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  )
}
```

---

#### Swift UI

```swift
struct ContentView: View {
    var body: some View {
        Text("Turtle Rock")
            .font(.title)
    }
}
```

<br/>

#### Flutter

```dart
class MyWidget extends StatelessWidget {
  final List<String> items;
  const MyWidget(this.items);
  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: items.length,
      itemBuilder: (context, index) {
        return ListTile(
          title: Text(items[index]),
        );
      },
    );
  }
}
```

---

### 命令式和声明式的区别

我们现在使用代码编程的方式就叫命令式

```kotlin
val textView = TextView(getContext())
textView.setText("Text")
textView.setColor()
textView.setTextSize()
addView(textView)
```

<br />

Compose 使用的是声明式

```kotlin
@Composable
fun Demo() {
    Column {
        Text(text = "Hello", fontSize = 18.sp, color = Color.Yellow)
    }
}
```

<!-- 它的特点是我们需要知道程序是如何运行的，我们需要用程序的方式去思考

比如说我们得新建一个 TextView，给它内容，颜色，大小，最后再将它添加到父 View 中

我们在写声明式的时候思维方式不一样，应该是描述我们想要这个 TextView 是什么样的，他的内容应该是什么，字体大小，颜色应该是什么

至于程序怎么实现，我们并不需要关心

这时候大家心里可能似懂非懂，有的人可能觉得和自己之前学的一种东西很像。[停顿两秒]

没错，就是 SQL 语言。
-->

---

有一些大家熟悉的语言本身就是声明式的，例如 SQL

```sql
SELECT * FROM Book
WHERE Genre = 'Science Fiction'  
ORDER BY Sales DESC
LIMIT 10;
```

<!-- 
我相信大家都不太知道数据库是怎么工作的，但是应该都会写 SQL 语句从数据库的某个表里拿出你想要的数据。比如说例子中描述的是从 Book 表中拿出最畅销的10本科幻小说。只需要描述我们想要的最终结果即可。

还有很多云原生的技术，比如 Kubernetes 是一个容器的编排系统，也是用的声明式来描述应用的目标状态，不过这里就太远了就不介绍了。

总结一下，声明式的优点就是简洁明了，我们不需要了解程序内部细节，只需要描述最终结果。不过大家需要知道声明式最终也是需要命令式去运行的， Compose 也只是在 Android 原生代码上包裹了一层语法糖。
-->

--- 

# Compose 的一些缺点

- ⌚️ 学习成本
- 🐛 没有踩过的坑
- 🛠 复杂页面难以使用

<!-- 
由于这是一套新的系统，需要一定时间去掌握，有学习成本。而且由于是新的东西，所以未来可能会遇到一些坑未完善。

还有就是一些复杂的页面比较难以使用 Compose 去编写，比如说 Cards 里的 Designer，我相信 FP 里也会有类似的复杂页面

最后咱们再看一下 Demo

这就是我对 Jetpack Compose 的介绍，相信大家已经对 Compose 有了比较大的兴趣，接下来请 Zech 来给大家介绍一下 Compose 的具体用法
 -->