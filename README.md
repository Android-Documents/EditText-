# EditText与虚拟键盘的问题

## EditText自动获得焦点并弹出软键盘

刚打开页面，界面未加载完全而无法弹出软键盘。需要设定一段延迟时间。

1. 在初始化EditText页面加入下面代码

```
Timer timer = new Timer();  
timer.schedule(new TimerTask() {  

    public void run() {  
        InputMethodManager inputManager = (InputMethodManager) editText.getContext().getSystemService(Context.INPUT_METHOD_SERVICE);  
        inputManager.showSoftInput(editText, 0);  
    }  

}, 500);
```

2. 给Activity配置加入下面属性

```
android:windowSoftInputMode="adjustResize"
```

## EditText不自动获取焦点

### 1. 在Manifest.xml文件中相应的Activity下添加如下代码：

```
android:windowSoftInputMode="stateHidden"
```

### 2. 让EditText失去焦点，用EditText的clearFocus：

```
EditText edt = (EditText)findViewById(R.id.edt);
edt.clearFocus();
```

### 3. 强制隐藏Android输入法窗口：

```
EditText edt = (EditText)findViewById(R.id.edt);  
InputMethodManager imm = (InputMethodManager)getSystemService(INPUT_METHOD_SERVICE);  
imm.hideSoftInputFromWindow(edt.getWindowToken(), 0);
```

### 4.要求EditText始终不弹出虚拟键盘：

```
EditText edt = (EditText)findViewById(R.id.edt);  
edt.setInputType(InputType.TYPE_NULL);
```
