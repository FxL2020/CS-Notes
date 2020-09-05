### 弹窗取消功能
1 隐藏弹窗
2 绑定的值置为空
```html
this.isPriceDialogShow = false;
this.priceAdjustmentDialog="";
```

### 弹窗确定功能
1 参数校验判断是否能为空
2 隐藏弹窗
3 定义一个参数接收表单的值
4 把表单绑定的值置为空
```html
  try {
          WhParameter.verifyNotEmpty(this.priceAdjustmentDialog, "调价依据");
        } catch (e) {
          this.$toast(e.message);//弹出调价依据不能为空的提示
          return;
        }
        this.isPriceDialogShow=false;
        this.priceAdjustmentBasis=this.priceAdjustmentDialog;
        this.priceAdjustmentDialog="";
```

### 弹窗修改功能
1 把值传给表单参数
2 打开弹窗
```html
this.priceAdjustmentDialog=this.priceAdjustmentBasis;
this.isPriceDialogShow=true;
```
