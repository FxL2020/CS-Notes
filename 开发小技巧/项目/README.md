### 弹窗修改功能
1 dialog里所有的属性都要赋值
2 打开弹窗
-->
1 重置dialog
2 隐藏弹窗
3 调用展示方法，展示数据<br>
dialog
```html
dialog: {
          id: "",
          operate: "ADD",
          employeeNum: "",
          name: "",
          sexName: "",
          sex: "",
          birthday: "",
          idCardNo: "",
        },
```
修改或添加弹窗
```html
 <!--弹窗，默认隐藏-->
    <div v-if="!isDialogAddOrModifyShow"
         @click="isDialogAddOrModifyShow = true"
         class="right_side_bar fold">添加
    </div>

    <div v-if="isDialogAddOrModifyShow" @click="closeDialog()"
         class="div_dialog"></div>
    <div v-show="isDialogAddOrModifyShow"
         class="cs_scrollable_vertical right_side_bar">
      <div class="content_dialog">
        <div class="info_dialog height_info_dialog">
          <div class="div_line_info">
            <div class="cs_text_default cs_align_left type_info_dialog">工号</div>
            <input v-model="dialog.employeeNum"
                   v-if="'ADD' === dialog.operate"
                   class="cs_text_default cs_padding_horizontal txt_info_dialog width_120"
                   placeholder="请输入">
            <!--修改弹窗 工号不可编辑-->
            <div v-if="'MODIFY' === dialog.operate"
                 class="cs_text_default cs_padding_horizontal txt_info_dialog width_120">
              {{dialog.employeeNum}}
            </div>
            <div class="cs_text_default cs_align_left type_info_dialog margin_left_29">姓名</div>
            <input v-model="dialog.name"
                   class="cs_text_default cs_padding_horizontal txt_info_dialog width_120"
                   placeholder="请输入">
          </div>
          <div class="ui_margin_top div_line_info">
            <div class="cs_text_default cs_align_left type_info_dialog">性别</div>
            <web-select v-model="dialog.sexName"
                        :options="SEX"
                        @option-key="updateSex"
                        class="cs_text_default cs_padding_horizontal txt_info_dialog width_120"></web-select>
            <div class="cs_text_default cs_align_left type_info_dialog margin_left_29">出生日期</div>
            <input id="birthday" v-model="dialog.birthday"
                   class="cs_text_default cs_padding_horizontal txt_info_dialog width_120"
                   type="text" readonly="readonly" placeholder="请选择">
          </div>
          <div class="ui_margin_top div_line_info">
            <div class="cs_text_default cs_align_left type_info_dialog">联系方式</div>
            <input v-model="dialog.phone" class="cs_text_default cs_padding_horizontal txt_info_dialog"
                   placeholder="请输入">
          </div>
          <div class="ui_margin_top div_line_info">
            <div class="cs_text_default cs_align_left type_info_dialog">身份证号</div>
            <input v-model="dialog.idCardNo" @keyup="checkIDNum($event)" maxlength="18" class="cs_text_default cs_padding_horizontal txt_info_dialog"
                   placeholder="请输入">
          </div>
          <button v-if="'ADD' === dialog.operate"
                  @click="confirmAdd()"
                  class="cs_text_default cs_radius ui_btn_common btn_add" type="button">添加
          </button>
          <button v-if="'MODIFY' === dialog.operate"
                  @click="confirmModify()"
                  class="cs_text_default cs_radius ui_btn_common btn_add" type="button">修改
          </button>
        </div>
      </div>
    </div>
```


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
