# 脑图和客服

## 使用方法

把以下脚本插入到body标签之后， 保存即可使用

```html

<script type="text/javascript">
  // 网页插件嵌入示例
  (function (w, d, s, i, v, j, b) {
    w[i] = w[i] || function () {
      (w[i].v = w[i].v || []).push(arguments)
    };
    j = d.createElement(s),
      b = d.getElementsByTagName(s)[0];
    j.async = true;
    j.charset = "UTF-8";
    j.src = "https://www.v5kf.com/123898/v5kf.js";
    b.parentNode.insertBefore(j, b);
  })(window, document, "script", "V5CHAT");

  // 调用V5CHAT接口示例（本例实现延迟10s显示对话按钮）
  V5CHAT('withoutBtn');       // 不显示浮动对话按钮
  V5CHAT('onPluginLoad', function () {
    // 插件加载完成的回调
    // setTimeout(function () {
    V5CHAT('showBtn');
    // 10s后显示浮动对话按钮
    // }, 10000);
  });
  // 指定人工服务示例
  V5CHAT('human', {
    human: 3,   // 指定客服模式:
    wid: 0,     // 指定的客服编号
    gid: 10001  // 指定的客服分组编号
  });

  // var isReady = false
  // V5CHAT('onReady', function() {
  //     // Your code here
  //     isReady = true
  // });


  var loading = false
  var timer
  function setMsg(msg) {
    if (loading) return
    timer && clearTimeout(timer)
    loading = true
    V5CHAT('showChat');
    if (!V5CHAT.isConnect) {
      V5CHAT('connect');
      V5CHAT('onConnect', function () {
        V5CHAT('msg', msg);
        V5CHAT('showChat');
        loading = false
      })
    } else {
      V5CHAT('msg', msg);
      loading = false
    }

    // 防止重复点击
    timer = setTimeout(function() {
      loading = false
    }, 500)
  }

</script>

<script>
  !(function () {

    document.removeEventListener('DOMContentLoaded', window.InitializeApplication)
    // var logoUrl = 'https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo_top_86d58ae1.png'
    // document.querySelector('.logo-img').setAttribute('src', logoUrl);

    window.InitializeApplication = function () {
      zip.useWebWorkers = !1;
      var a = document.getElementById("app").textContent;
      zip.createReader(new zip.Data64URIReader("data:application/zip;base64," + a), function (a) {
        a.getEntries(function (a) {
          var b = document.getElementById("bootstrap-loader")
            , c = document.getElementById("bootstrap-progress-bar")
            , d = {
              "viewer.js": 0,
              "viewer.css": 0
            }
            , e = null
            , f = -10;
          a.forEach(function (a) {
            var g = a.filename;
            a.getData(new zip.TextWriter, function (a) {
              switch (g) {
                case "viewer.js":
                  b.parentNode.removeChild(b);
                  var c = eval;
                  c(a),
                    "undefined" != typeof ga && (ga("create", mm.config.ga.trackingId, "auto"),
                      ga("set", "checkProtocolTask", null),
                      ga("set", "checkStorageTask", null),
                      ga("set", "historyImportTask", null))
                      // mm.Analytics = {},
                      // mm.Analytics.track("Share_HTML5_Export_View_V2"));

                  // document.querySelector('.logo-img').setAttribute('src', logoUrl);
                  setTimeout(function() {
                    var $tooltip = document.querySelector('[data-tooltip="菜单"]')
                    var $toolbar = document.querySelector('.toolbar-logo')
                    $tooltip && $tooltip.remove();
                    $toolbar && $toolbar.remove();
                  })
                  
                  function handleClickNode(e) {
                    console.log($(e.currentTarget).find('tspan').text())
                    // alert($(e.currentTarget).find('tspan').text())
                  }
                  mm.paper.on('cell:pointerclick', function (elementView) {
                    var nodeText = elementView.model.wrappedText;
                    setMsg(nodeText)
                  });

                  break;
                case "viewer.css":
                  var d = document.createElement("style");
                  d.setAttribute("type", "text/css"),
                    d.textContent = a,
                    document.head.appendChild(d)
              }
            }, function (a, b) {
              if (g !== e && (e = g,
                f += 10),
                a > d[g] && f >= 0) {
                d[g] = a;
                var h = f + 10 * (a / b) + "%";
                c.style.width = h
              }
            })
          })
        })
      })
    }

    document.addEventListener('DOMContentLoaded', window.InitializeApplication)
  })()
</script>
```
