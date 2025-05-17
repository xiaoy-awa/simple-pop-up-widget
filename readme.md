# 高级弹窗组件文档

这是一个功能丰富的弹窗通知组件，支持多种类型的弹窗，包括成功、错误、警告、公告以及输入弹窗。该组件提供了丰富的自定义选项，并支持深色/浅色主题切换。

## 目录

- [基本使用](#基本使用)
- [弹窗类型](#弹窗类型)
  - [成功弹窗](#成功弹窗)
  - [错误弹窗](#错误弹窗)
  - [警告弹窗](#警告弹窗)
  - [公告弹窗](#公告弹窗)
  - [输入弹窗](#输入弹窗)
- [高级功能](#高级功能)
  - [固定弹窗](#固定弹窗)
  - [主题切换](#主题切换)
  - [按钮控制](#按钮控制)
- [API参考](#api参考)
  - [showAlert函数](#showalert函数)
  - [showInputAlert函数](#showinputalert函数)
- [使用示例](#使用示例)
  - [基本弹窗示例](#基本弹窗示例)
  - [输入弹窗示例](#输入弹窗示例)
- [获取输入弹窗结果](#获取输入弹窗结果)
  - [Promise方法的优势](#promise方法的优势)
  - [链式调用示例](#链式调用示例)
  - [表单处理示例](#表单处理示例)
- [浏览器兼容性](#浏览器兼容性)
- [响应式设计](#响应式设计)
- [性能优化](#性能优化)

## 基本使用

该弹窗组件易于使用，只需引入相关的CSS和JavaScript文件，然后调用对应的函数即可。

```html
<link rel="stylesheet" href="alert.css">
<script src="alert.js"></script>

<script>
  // 显示一个成功弹窗
  showAlert('操作成功完成！', 'success');
</script>
```

## 弹窗类型

### 成功弹窗

成功弹窗用于通知用户操作已成功完成。具有绿色主题和勾号图标。

```javascript
showAlert('操作成功完成！', 'success');
```

![成功弹窗效果图](https://backup.xiaoy.asia/data/success.png)
![成功弹窗效果图2](https://backup.xiaoy.asia/data/success_dark.png)

#### 成功弹窗特点

- 绿色主题
- 对勾图标
- 平滑弹出和淡出动画

### 错误弹窗

错误弹窗用于通知用户操作失败或发生错误。具有红色主题和叉号图标。

```javascript
showAlert('操作失败，请重试！', 'error');
```

![错误弹窗效果图](https://backup.xiaoy.asia/data/error.png)
![错误弹窗效果图2](https://backup.xiaoy.asia/data/error_dark.png)

#### 错误弹窗特点

- 红色主题
- 叉号图标
- 平滑弹出和淡出动画

### 警告弹窗

警告弹窗用于向用户发出需要注意的信息。具有黄色主题和感叹号图标。

```javascript
showAlert('请注意，此操作需要谨慎！', 'warning');
```

![警告弹窗效果图](https://backup.xiaoy.asia/data/warning.png)
![警告弹窗效果图2](https://backup.xiaoy.asia/data/warning_dark.png)

#### 警告弹窗特点

- 黄色主题
- 感叹号图标
- 平滑弹出和淡出动画

### 公告弹窗

公告弹窗用于传达系统公告或重要通知。具有蓝色主题和喇叭图标。

```javascript
showAlert('欢迎使用本系统，有新功能上线！', 'announcement');
```

![公告弹窗效果图](https://backup.xiaoy.asia/data/announcement.png)

#### 公告弹窗特点

- 蓝色主题
- 喇叭图标
- 平滑弹出和淡出动画
- 注：公告不区分黑白页面切换

### 输入弹窗

输入弹窗提供了用户输入文本的界面，支持必填和可选两种模式。

```javascript
showInputAlert('请输入内容', '在此处输入...', {
  onConfirm: function(text) { 
    showAlert('您输入了: ' + text, 'success'); 
  }
});
```

![输入弹窗效果图](https://backup.xiaoy.asia/data/input.png)

#### 输入弹窗特点

- 提供文本输入框
- 支持必填输入模式
- 确认和取消按钮
- 可选的关闭按钮
- 支持背景点击关闭（非必填模式）

## 高级功能

### 固定弹窗

弹窗可以被固定在屏幕顶部，防止自动关闭。固定的弹窗会一直保持在屏幕上，直到用户手动关闭。

### 主题切换

弹窗组件支持深色和浅色主题切换，可以适应网站的整体风格。

![浅色主题弹窗效果图](https://backup.xiaoy.asia/data/input.png)
![深色主题弹窗效果图](https://backup.xiaoy.asia/data/input_dark.png)

#### 主题切换特点

- 支持浅色/深色主题自动适配
- 渐变过渡动画
- 支持从按钮向四周扩散的切换效果
- 支持从四周向按钮收缩的切换效果

### 按钮控制

弹窗提供了可自定义的关闭和固定按钮，可以根据需要显示或隐藏这些按钮。

![带按钮的弹窗效果图](https://backup.xiaoy.asia/data/input_2.png)

## API参考

### showAlert函数

```javascript
/**
 * 显示弹窗通知
 * @param {string} message - 消息内容，默认为"操作失败，请重试"
 * @param {string} type - 弹窗类型，可以是"error"、"success"、"warning"或"announcement"，默认为"error"
 * @param {object} options - 配置选项
 * @param {boolean} options.showCloseButton - 是否显示关闭按钮，默认为true
 * @param {boolean} options.showPinButton - 是否显示固定按钮，默认为true
 * @returns {HTMLElement} - 返回创建的弹窗元素
 */
function showAlert(message, type, options) {}
```

### showInputAlert函数

```javascript
/**
 * 显示输入弹窗
 * @param {string} title - 弹窗标题，默认为"标题"
 * @param {string} placeholder - 输入框占位文本，默认为"请输入文字..."
 * @param {object} options - 配置选项
 * @param {boolean} options.required - 是否必须输入，默认为false
 * @param {boolean} options.showCloseButton - 是否显示关闭按钮，默认与required相反
 * @param {boolean} options.clearPinnedAlerts - 是否清除固定的弹窗，默认为false
 * @param {function} options.onConfirm - 确认按钮回调函数，参数为输入的文本
 * @param {function} options.onCancel - 取消按钮回调函数
 * @returns {HTMLElement} - 返回创建的弹窗元素
 */
function showInputAlert(title, placeholder, options) {}
```

## 使用示例

### 基本弹窗示例

```javascript
// 显示成功弹窗
showAlert('操作成功完成！', 'success');

// 显示错误弹窗
showAlert('操作失败，请重试！', 'error');

// 显示警告弹窗
showAlert('请注意，此操作需要谨慎！', 'warning');

// 显示公告弹窗
showAlert('欢迎使用本系统，有新功能上线！', 'announcement');

// 自定义按钮显示
showAlert('只显示关闭按钮', 'success', {showCloseButton: true, showPinButton: false});
```

### 输入弹窗示例

```javascript
// 显示普通输入弹窗
showInputAlert('请输入内容', '在此处输入...', {
  onConfirm: function(text) { 
    console.log('确认输入:', text); 
  },
  onCancel: function() { 
    console.log('取消输入'); 
  }
});

// 显示必填输入弹窗
showInputAlert('必填内容', '此处必须输入内容...', {
  required: true,
  onConfirm: function(text) { 
    console.log('确认输入:', text); 
  }
});

// 显示输入弹窗并清除固定弹窗
showInputAlert('重要输入', '请输入内容...', {
  clearPinnedAlerts: true,
  onConfirm: function(text) { 
    console.log('确认输入:', text); 
  }
});
```

## 获取输入弹窗结果

如果需要在不修改alert.js的情况下获取输入弹窗的结果，可以使用Promise包装showInputAlert函数。以下是一个简单的实现方式：

```javascript
// 使用Promise包装showInputAlert函数，以获取用户输入
function getInputValue(title = "请输入", placeholder = "请在此处输入...") {
  return new Promise((resolve, reject) => {
    // 调用showInputAlert函数并传递onConfirm回调
    showInputAlert(title, placeholder, {
      onConfirm: function(value) {
        // 当用户点击确认时，通过resolve返回输入值
        resolve(value);
      },
      onCancel: function() {
        // 当用户点击取消时，通过reject返回取消消息
        reject(new Error('用户取消了输入'));
      }
    });
  });
}

// 使用示例
async function testInput() {
  try {
    // 异步等待用户输入
    const result = await getInputValue("请输入您的姓名", "例如：张三");
    console.log("用户输入的内容是:", result);
    
    // 使用输入结果
    showAlert(`您好，${result}！`, 'success');
    
    // 或者将结果显示在页面上
    document.getElementById('result').textContent = `您输入的内容是: ${result}`;
  } catch (error) {
    console.log("输入被取消:", error.message);
    showAlert("输入已取消", 'warning');
  }
}
```

### Promise方法的优势

使用Promise包装输入弹窗有以下优势：

1. **优雅的异步处理**：可以使用async/await语法，使代码更加清晰
2. **更好的错误处理**：可以使用try/catch结构处理用户取消输入的情况
3. **链式处理**：可以使用.then().catch()链式处理输入结果
4. **与现代JavaScript框架兼容**：更容易集成到React、Vue等现代框架中

### 链式调用示例

也可以使用链式调用方式处理输入结果：

```javascript
getInputValue("请输入您的评论", "我想说...")
  .then(comment => {
    showAlert(`感谢您的评论: ${comment}`, 'success');
    return getInputValue("请留下您的联系方式", "手机号或邮箱");
  })
  .then(contact => {
    showAlert(`我们会通过 ${contact} 联系您`, 'success');
  })
  .catch(error => {
    showAlert("操作已取消", 'warning');
  });
```

### 表单处理示例

结合Promise方法可以轻松处理多步表单输入：

```javascript
async function processForm() {
  try {
    const name = await getInputValue("请输入您的姓名");
    const age = await getInputValue("请输入您的年龄");
    const email = await getInputValue("请输入您的邮箱");
    
    // 处理所有输入结果
    showAlert(`表单提交成功！\n姓名: ${name}\n年龄: ${age}\n邮箱: ${email}`, 'success');
  } catch (error) {
    showAlert("表单提交已取消", 'warning');
  }
}
```

## 浏览器兼容性

该弹窗组件兼容所有现代浏览器，包括：

- Chrome (最新版)
- Firefox (最新版)
- Safari (最新版)
- Edge (最新版)

## 响应式设计

弹窗组件采用响应式设计，会根据屏幕尺寸自动调整大小和布局，在移动端和桌面端都能提供良好的用户体验。

## 性能优化

该组件经过性能优化，即使在同时显示多个弹窗的情况下也能保持流畅的动画效果和良好的性能。
