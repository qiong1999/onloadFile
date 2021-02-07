## HTML5 显示上传的图片和文件

新增的 File API 允许 JavaScript 读取文件内容，本文主要展示如何在前端页面显示上传的图片和视频

图片预览：

![上传前](./image/上传前.png)
![上传后](./image/上传后.png)

### 代码

```javascript

      //获取input节点和显示文件的父节点
      let file = document.getElementById("file");
      let show = document.getElementById("show");
      //监听input节点的onchange事件
      file.onchange = function (e) {
        //e.target.files[0]获取上传的文件
        let currentFile = e.target.files[0];

        showImage(currentFile);
      };

      function showImage(file) {
        //读取文件
        let reader = new FileReader();
        //设置回调函数
        reader.onload = function (e) {
            /*reader.readAsDataURL()会发起一个异步操作来读取文件内容
            当文件读取完成后，自动调用这个函数*/
          if (
            file.type === "image/jpeg" ||
            file.type === "image/png" ||
            file.type === "image/gif"
          ) {
            show.innerHTML = `<img src=${e.target.result} alt=图片 />`;
          } else if(file.type="video/mp4"||file.type="video/mp3){
            show.innerHTML = `<video src=${e.target.result} autoplay muted />`
          }
        };
        //以DataURL的形式读取文件
        reader.readAsDataURL(file);
      }
```
