# PPMessage 配置指南

> 以下介绍如何在网站或应用里配置 PPMessage。

## 自定义 PPMessage 聊天组件
可以轻松自定义PPMessage 聊天组件，使其与您的产品或网站浑然一体。在自定义过程中，您可以访问“设置-开发者设置-网络聊天链接”查看设置是否满足您的需要。



### 设置聊天组件颜色
访问 “设置-开发者设置-网页聊天插件”，选择合适的颜色后，点击下图箭头所示“select”按钮，您网站的聊天按钮和组件窗口颜色将变成所选的颜色.

### 设置聊天组件上显示的团队信息
通过更改后台的团队设置信息，您可以控制聊天组件上向您的访客展示的团队名称和默认欢迎语。 访问 “设置-团队设置-团队设置”。点击修改团队设置界面的“公司简称”和“默认欢迎语”，聊天组件上对应的展示信息就会发生相应的变化。

### 聊天组件高级定制方法
通过编辑‘网页聊天插件’的‘网站插件代码’可以实现对 PPMessage 聊天图标和聊天对话窗口的更多控制。您需要将编辑后的网页插件代码粘贴到您的网站页面与标签之间。

让我们把插件代码的格式变的好看些:

```
<script> 
window.ppSettings = {
  app_uuid:'a600998e-efff-11e5-9d9f-02287b8c0ebf'
};
(function(){
  var w=window,d=document;
  function l() {
    var a=d.createElement('script');
    a.type='text/javascript';
    a.async=!0;
    a.charset='utf-8';
    a.src='https://ppmessage.cn/ppcom/assets/pp-library.min.js';
    var b=d.getElementsByTagName('script')[0];
    b.parentNode.insertBefore(a,b)
  }
  l();
})();
</script>
```

改变聊天按钮的位置
默认情况下聊天按钮的位置在整个网页的右下角，改变聊天按钮的位置需要在 ppSettings 中增加一些控制信息:

```
<script> 
window.ppSettings = {
  app_uuid:'a600998e-efff-11e5-9d9f-02287b8c0ebf',
  view: {
    launcher_is_show: true,
    launcher_bottom_margin: '20px',
    launcher_right_margin: '30px',
    launch_style: {
      mode: 'normal',
      position:'right',
      bottom: 95
    }
  }
};
(function(){
  var w=window,d=document;
  function l() {
    var a=d.createElement('script');
    a.type='text/javascript';
    a.async=!0;
    a.charset='utf-8';
    a.src='https://ppmessage.cn/ppcom/assets/pp-library.min.js';
    var b=d.getElementsByTagName('script')[0];
    b.parentNode.insertBefore(a,b)
  }
  l();
})();
</script>
```

这些控制信息都是默认值，就是说不控制就是这样的。 其中 `launcher_bottom_margin` 和 `launcher_right_margin` 是用来控制聊天按钮距离浏览器窗口右边和底边的距离，更改这个大小，看看效果吧。

不过仅仅改这个聊天图标的位置是不够的，PPMessage 还没有那么智能，点击聊天图标后，聊天对话窗口还是从默认的右下窗口弹出，这个效果可能不是你想要的，这时候需要继续更改窗口位置。

改变聊天窗口的位置
还是刚才的代码，控制聊天窗口位置的是 `view.launch_style.position/bottom`，分别表示聊天窗口是在浏览器的左侧还是右侧，以及距离浏览器的底边高度。如果应用自定义的 `lauch_style`，需要将 `lauch_style.mode` 指定为 `custom`。应用了自定义的风格，聊天对话的窗口弹出动画方式自动改变。`position` 可以取的值有 `left/right/center`； 如果 `position` 为 `right` 那么聊天窗口将从浏览器的右侧滑出，如果是 `center`，那么聊天窗口将从页面中间淡出，并且居于页面中间。

```
window.ppSettings = {
  app_uuid:'a600998e-efff-11e5-9d9f-02287b8c0ebf',
  view: {
    launcher_bottom_margin: '200px',
    launcher_right_margin: '30px',
    launcher_is_show: true,
    launch_style: {
      mode: 'custom',
      position:'right',
      bottom: 295
    }
  }
};
(function(){
  var w=window,d=document;
  function l() {
    var a=d.createElement('script');
    a.type='text/javascript';
    a.async=!0;
    a.charset='utf-8';
    a.src='https://ppmessage.cn/ppcom/assets/pp-library.min.js';
    var b=d.getElementsByTagName('script')[0];
    b.parentNode.insertBefore(a,b)
  }
  l();
})();
```

自己尝试实验一下吧。

还有一个你想改变的，就是改变聊天按钮的图标。

隐藏聊天按钮的图标
隐藏聊天按钮的图标需要一个新的变量，`launcher_is_show`，赋予它 `true` 或者 `false`，即可控制显示聊天按钮或者隐藏聊天按钮，`true` 就是显示，`false` 就是隐藏。

```
window.ppSettings = {
  app_uuid:'a600998e-efff-11e5-9d9f-02287b8c0ebf',
  view: {
    launcher_bottom_margin: '200px',
    launcher_right_margin: '30px',
    launcher_is_show: false,
    launch_style: {
      mode: 'custom',
      position:'right',
      bottom: 295
    }
  }
};
(function(){
  var w=window,d=document;
  function l() {
    var a=d.createElement('script');
    a.type='text/javascript';
    a.async=!0;
    a.charset='utf-8';
    a.src='https://ppmessage.cn/ppcom/assets/pp-library.min.js';
    var b=d.getElementsByTagName('script')[0];
    b.parentNode.insertBefore(a,b)
  }
  l();
})();
```

值得注意的是 `launcher_is_show` 不是必须与 `custom mode` 一起使用。

下面你一定需要打开关闭聊天窗口的接口了，因为聊天按钮已经被隐藏了，本来打开和关闭聊天窗口是它来完成的。

### 打开、关闭聊天窗口
您可是在网页的其他位置使用 Javascript 调用 `PP.show()` 去打开聊天窗口，`PP.hide()` 去关闭聊天窗口，唯一需要注意的是一定要在 `PP` 对象已经存在的情况下使用。

开发者可以在处理指定元素的 `click、hover` 等事件的时机来调用 `PP.show()` 或者 `PP.hide()`。如果想了解 PPMessage 的聊天窗口的打开状态可以用 `PP.isOpen()` 来检查，如果正在使用类似 `angularjs` 这样的前端框架，可以用 `ng-if` 来绑定不同的界面操作按钮。 开发者也可以通过`PP` 对象的 `onHide` 和 `onShow` 来响应聊天窗口打开和关闭的事件，通过回调函数来控制自己的界面显示:

```

PP.onHide(function() {
});


PP.onShow(function() {
})
```

## 配置客服团队

缺省情况下，PPMessage 将所有座席人员视为一个大的工作组。访客咨询消息不需要排队，立刻接入系统，座席人员都可以看到新进入的消息，也能看到是否有其他团队成员正在处理，这种模式的接待能力远远高于目前市面上需要消息排队的同类产品。您也可以根据业务需求，将客服分成多个工作组，并将消息在工作组间分配。创建客服团队，首先需要添加座席人员。

### 管理座席人员
访问 “设置-团队设置-座席人员”,点击“添加”按钮，您就可以依次添加座席人员了。

需要注意的是，PPMessage 通过邮件地址标识新增座席人员，请务必为新增座席人员设置真实的邮件地址。否则新增座席人员密码丢失将无法找回。 座席人员添加完成后，您可以为他们建立不同的组织。

### 管理座席组织
座席组织是管理您的客服人员在 PPMessage 中一起工作的好办法。您可以将对话分配给一个座席组织，而不是单个座席人员。每个座席组织的成员都可以轻松查看和管理分配给该组织的对话。

访问“设置-团队设置-座席组织”，点击“添加”按钮可以创建新的客服组。

点击新添加的座席组织图标后，单击右边栏“成员”项左侧的箭头图标，出现“+” 和“-”按钮，点击“+”按钮，就可以为新的座席组织添加成员了。

### 配置客户信息
在 PPMessage 中可以查看，过滤，搜索和细分客户，可以让您轻松了解每个访客并可以统计分析不同访客群体的行为特征。您可以根据您的业务需要，在 PPMessage 设置特定于您的用户群的自定义用户属性和用户事件。您可以在与客户聊天时记录这些自定义用户属性，也可以通过 Javascript 代码将这些信息推送给 PPMessage。这些属性将和 PPMessage 的标准字段一起出现在 PPMessage 访客界面的过滤条件列表里，您可以利用这些属性进行客户细分。

## 设置通过微信接收离线消息
如果您希望在离线的情况下仍可以接收访客消息并进行回复，您需要使用坐席服务人员的微信去关注 PPMessage 的公众号。然后将坐席服务人员的微信和 PPMessage 系统中的坐席服务人员账号密码绑定。

点击绑定座席，输入坐席服务人员在 PPMessage 的注册邮箱和密码，微信提示座席绑定成功后，您就可以通过微信接收和回复访客消息了。

这样即使您的坐席服务人员没有登录 PPMessage 的后台系统，访客发送的消息会自动通过 PPMessage 公众号推送到您的坐席服务人员的微信上。
