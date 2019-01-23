### 自定义View

```
//方法一
public MyView(Context context) {
    super(context);
}
//方法二
public MyView(Context context, AttributeSet attrs) {
    super(context, attrs);
}
```

如果这个控件会在 java 代码中 new 的话，必须实现方法一，如果控件直接在 xml 中使用，必须实现方法二，两者至少实现一个。
有的时候，可以简单粗暴点，把方法一中的 super(context) 改成 this(context,null)。
当然，什么情况下可以这么做就不阐述了，下面我们还是介绍下关于　AttributeSer这个参数把。

#### AttributeSer - 自定义属性
每个控件都会有属性，既然是自定义控件怎么能少了自定义属性呢！ １．为了方便展开话题，我们先照做在 res/values/ 目录下添加一个 attrs.xml 这个文件。
```
attrs.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- 这里会写什么呢！，当然是我们的自定义属性 -->
    <declare-styleable name="MyViewStyle" >
           <declare-styleable name="MyViewStyle" >
            <attr name="content" format="string" />
            <attr name="isShow" format="boolean"/>
            <attr name="background" format="color"/>
            <attr name="select" >
                <flag name="s1" value="１"/>
                <flag name="s2" value="2"/>
                <flag name="s3" value="3"/>
            </attr>
    </declare-styleable>
</resources>
```

#### 自定义控件 - View - onMeasure
既然是一个控件，啥都别说，肯定要先有他的宽高，但是我们明明已经在xml中定义了控件的 layout_widght 与 layout_height，为什么还要特地重写自定义控件的。至于为什么请看下面。

几个概念

Android 系统给我们提供了一个　MeasureSpec类，通过它来帮助我们测量 View，MeasureSpec 是一个 32 的 int 值，其中高 ２ 为为测量模式，低30位为测量的大小，这难道是二进制！是的，但是大可放心，google 还是挺为广大数学渣着想的，通过 MeasureSpec 的方法可以获取我们需要的数值。

再来说说测量模式把，测试模式可以为一下三种：

EXACTLY:精确模式 当我们将控件的 layout_width 与 layout_height 属性制定为具体数值时(排除 wrap_content)，系统就使用这个模式，(同时 View 类的 onMeasure 默认是 EXACTLY 模式，所以不重写 onMeasure 的话，就只能使用默认模式)

AT_MOST:最大值模式 当控件的 layout_width 属性或 layout_height 属性为 wrap_content 时，控件大小一般随着子控件或内容的变化而变化，此时控件的此尺寸只要不超过父控件允许的最大尺寸。

UNSPECIFIED： 它不能其大小测量模式，View想多大就多大，通常情况在回执自定义View时才使用。
```
@Override
protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
    super.onMeasure(widthMeasureSpec, heightMeasureSpec);
    //设置控件的宽高，记住这里默认是px，记得要分辨率转换实现适配，这里不做说明
    setMeasuredDimension(getSize(widthMeasureSpec),getSize(heightMeasureSpec));
}
 
private int getSize(int measureSpec){
    int result = 0;
    int specMode = MeasureSpec.getMode(measureSpec);
    int specSize = MeasureSpec.getSize(measureSpec);
    switch (specMode){
        case MeasureSpec.EXACTLY:
            //当layout_width与layout_height　match_parent 为固定数值走这里
            result = 200;
            break;
        case MeasureSpec.AT_MOST:
            //当layout_width与layout_height定义为 wrap_content　就走这里
            result = Math.min(１00,specSize);
            break;
        case MeasureSpec.UNSPECIFIED:
            //如果没有指定大小
            result = 400;
            break;
    }
    return result;
}
```

#### 自定义控件 - View - layout
layout，顾名思义，就是定义这个控件所处的布局，其实即便我们通过 onMeasure 决定了这个控件的宽高，但是并不是所有的宽高都是能显示出来的，我们还需要通过 layout 给这个控件分配可以使用的控件。

因为 layout 不难，理解即可，所以毫不客气的直接上代码了。

@Override
public void layout(int l, int t, int r, int b) {
    super.layout(l, t, r, b);
    Log.d("layout:","l:"+l);
    Log.d("layout:","t:"+t);
    Log.d("layout:","r:"+r);
    Log.d("layout:","b:"+b);
}
这4个参数的意义分别是：距左距离、距顶距离、距右距离、距底距离

#### 自定义控件 - View - onDraw
该准备的准备了，不该说的也说了，接下来就就是要重写的我们的onDraw方法，既然是自定义View，无非就是显得'花销'一点，定制性高点，那么onDraw方法非调用不可。

View的绘制离不开 Canvas，所以在重写 onDraw 方法的时候，系统传递给我们一个 Canvas 对象，剩下的就是配合一个自己创建的 Paint 去绘制我们想要的界面。
```
@Override
protected void onDraw(Canvas canvas) {
    super.onDraw(canvas);
    Paint paint = new Paint();
    canvas.drawCircle(50, 50, 50, paint);
}
```
##### invalidate 方法是刷新 View


