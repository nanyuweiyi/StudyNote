
Android调用JS代码：

1、通过webview的loadUrl();

2、通过webview的evaluateJavascript();

```
// Android版本变量
final int version = Build.VERSION.SDK_INT;
// 因为该方法在 Android 4.4 版本才可使用，所以使用时需进行版本判断
if (version < 18) {
    mWebView.loadUrl("javascript:callJS()");
} else {
    mWebView.evaluateJavascript（"javascript:callJS()", new ValueCallback<String>() {
        @Override
        public void onReceiveValue(String value) {
            //此处为 js 返回的结果
        }
    });
}
```


特别注意：JS代码调用一定要在 onPageFinished（） 回调之后才能调用，否则不会调用。




JS调用Android的代码：

1、通过webview的addJavascriptInterface(new JSInterface(), "jsInterface");进行对象映射；

2、通过webview的shouldOverrideUrlLoading()回调拦截url;


