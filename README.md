# html-qrcode-vue
html网页扫码页面 zxing
二维码扫码 github

https://github.com/zxing-js/library

https://gitee.com › aliwean › NBZxing
NBZxing: 2020年最好用的开源扫码，全方位优化 ... - Gitee

zxing网页

前端实现扫一扫，扫描二维码（VUE，H5）；jsQR，zxing两种方式_前端二维码识别-CSDN博客https://blog.csdn.net/Gy_gsdsb/article/details/144417638




搜索http-server https

用
pkg install openssl-tool
然后下面命令会生成 cert.pem和key.pem俩文件，命令中可以直接用名字，或者用完整路径，如果用名字就是当前主目录，会生成这俩文件，
同理http-server -S -C cert.pem -o，这里也如果用cert.pem就是 cert.pem，如果是路径就写路径


# 首先使用以下命令生成一个证书密钥对 key.pem 和 cert.pem，它将有效期约10年（准确地说是3650天）
openssl req -newkey rsa:2048 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem
# 然后便可以起服务了 下面两个命令都可以，后者会自动打开默认浏览器运行页面
http-server -S
http-server -S -C cert.pem -o

参考：
作者：sunxiaochuan
链接：https://www.jianshu.com/p/7895c57a321c
來源：简书 使用 http-server 在本地开启 https 服务
https://www.cnblogs.com/DreamSeeker/p/16468040.html
http-server在本地启动https服务以及配置域名

要不然会报错can't enumerate devices, method not supported · Issue #225 · zxing-js/library · GitHub
https://github.com/zxing-js/library/issues/225

vue3+vite+@zxing/library实现移动端浏览器扫描二维码&条形码
https://juejin.cn/post/7345644573651714088

pnpm i @vitejs/plugin-basic-ssl -D

把下面vite.config.ts
```
import basicSsl from '@vitejs/plugin-basic-ssl'

export default { 
server: { 
https: true 
}, 
plugins: [ basicSsl() ] 
}
```
内容添加到
https://cn.vuejs.org/guide/quick-start（vue文件中）

运行npm create vue@latest之后生成的默认vite.config.ts中
应该是 npm init vite@latest
https://www.vitejs.net/guide/#scaffolding-your-first-vite-project
（vite创建）

```
#这个是默认vite.config.ts
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueDevTools from 'vite-plugin-vue-devtools'

// https://vite.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    vueDevTools(),
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    },
  },
})

```

得到

```
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueDevTools from 'vite-plugin-vue-devtools'
import basicSsl from '@vitejs/plugin-basic-ssl'

// https://vite.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    basicSsl(),  // Add the basicSsl plugin here
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    },
  },
  server: {
    https: true,  // Enable HTTPS
  },
})
```

把原文章app.vue文件变成html项目
https://github.com/copilot/c/3ff43558-b38b-4b8a-9f9c-ba5e516ba0d5

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Camera QR Code Scanner</title>
    <style>
        .root {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .content {
            width: 100%;
        }

        .camera {
            height: 50vh;
            position: relative;
        }

        #video {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .border {
            position: absolute;
            top: 0;
            height: 100%;
            width: 100%;
            display: grid;
            grid-template-columns: 1fr 1fr 1fr 1fr;
            grid-template-rows: 1fr 1fr 1fr 1fr;
            grid-template-areas:
                'a a a a'
                'b e e c'
                'b e e c'
                'd d d d';
        }

        .plate-rank-content {
            box-shadow: inset 0px 0px 10px 0px rgba(32, 116, 247, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.4);
            position: relative;
        }

        .solid {
            width: 95%;
            height: 1px;
            position: absolute;
            background-color: rgb(0, 119, 255);
            border-radius: 6px;
            animation: 1.5s linear 0s infinite alternate move_eye;
            left: 50%;
            transform: translateX(-50%);
        }

        @keyframes move_eye {
            0% {
                top: 3px;
            }

            50% {
                top: 50%;
            }

            100% {
                top: calc(100% - 6px);
            }
        }

        .angle-border {
            position: absolute;
            width: 24px;
            height: 24px;
        }

        .left-top-border {
            top: -3px;
            left: -3px;
            border-left: 3px solid red;
            border-top: 3px solid red;
        }

        .right-top-border {
            top: -3px;
            right: -3px;
            border-right: 3px solid red;
            border-top: 3px solid red;
        }

        .left-bottom-border {
            bottom: -3px;
            left: -3px;
            border-bottom: 3px solid red;
            border-left: 3px solid red;
        }

        .right-bottom-border {
            bottom: -3px;
            right: -3px;
            border-right: 3px solid red;
            border-bottom: 3px solid red;
        }

        .item {
            background-color: rgba(128, 128, 128, .3);
        }

        .item-1 {
            grid-area: a;
        }

        .item-2 {
            grid-area: b;
        }

        .item-3 {
            grid-area: c;
        }

        .item-4 {
            grid-area: d;
        }

        .item-5 {
            grid-area: e;
        }

        .btn {
            text-align: center;
            margin-top: 10px;
        }

        .primary-btn {
            background-color: #0077ff;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
        }

        .primary-btn:hover {
            background-color: #005bb5;
        }
    </style>
</head>
<body>
    <div class="root">
        <div class="content">
            <div class="camera">
                <video id="video" autoplay></video>
                <div class="border">
                    <div class="item-1 item"></div>
                    <div class="item-2 item"></div>
                    <div class="item-3 item"></div>
                    <div class="item-4 item"></div>
                    <div class="plate-rank-content item-5">
                        <div class="angle-border left-top-border"></div>
                        <div class="angle-border right-top-border"></div>
                        <div class="angle-border left-bottom-border"></div>
                        <div class="angle-border right-bottom-border"></div>
                        <div class="solid"></div>
                    </div>
                </div>
            </div>
            <div class="btn">
                <button type="button" id="open-camera" class="primary-btn">
                    开始扫码
                </button>
            </div>
        </div>
    </div>

    <script src="https://unpkg.com/@zxing/library@latest"></script>
    <script>
        document.addEventListener('DOMContentLoaded', (event) => {
            const codeReader = new ZXing.BrowserMultiFormatReader();
            console.log('ZXing code reader initialized');

            const openScan = async () => {
                try {
                    const videoInputDevices = await codeReader.listVideoInputDevices();
                    console.log("videoInputDevices", videoInputDevices, "摄像头设备");

                    // 默认获取第一个摄像头设备id
                    const firstDeviceId = videoInputDevices[0].deviceId; // 根据id选择摄像头
                    decodeFromInputVideoFunc(firstDeviceId);
                } catch (err) {
                    alert(err);
                }
            };

            const decodeFromInputVideoFunc = (firstDeviceId) => {
                // decodeFromInputVideoDeviceContinuously 已弃用，使用 decodeFromVideoDevice
                // firstDeviceId为null 时默认选择面向环境的摄像头
                codeReader.decodeFromVideoDevice(firstDeviceId, "video", (result, err) => {
                    if (result) {
                        console.log(result, "扫描结果");
                    }
                    if (err && !err) {
                        console.error(err);
                    }
                });
            };

            document.getElementById('open-camera').addEventListener('click', openScan);

            window.addEventListener('beforeunload', () => {
                codeReader.reset();
            });
        });
    </script>
</body>
</html>
```

# 下面是第二种方法
@zxing/library
例子项目 https://zxing-js.github.io/library/
源代码为一个html，
https://github.com/zxing-js/library/tree/master/docs/examples/
：

```
<!doctype html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="author" content="ZXing for JS">

    <title>ZXing TypeScript | Decoding from image file</title>

    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null" href="https://fonts.googleapis.com/css?family=Roboto:300,300italic,700,700italic">
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null" href="https://unpkg.com/normalize.css@8.0.0/normalize.css">
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null" href="https://unpkg.com/milligram@1.3.0/dist/milligram.min.css">
</head>

<body>

    <main class="wrapper" style="padding-top:2em">

        <section class="container" id="demo-content">
            <h1 class="title">Scan 1D/2D Code from Image</h1>

            <p>
                <a class="button-small button-outline" href="../../index.html">HOME 🏡</a>
            </p>

            <p>
                This example shows how to scan any supported 1D/2D code with ZXing javascript library from an image.
                The example decodes from the
                <code>src</code> in
                <code>img</code> tag, however is also possible to decode directly from an url without an
                <code>img</code> tag.
            </p>

            <div>
                <a class="button" id="decodeButton">Decode</a>
            </div>

            <div>
                <img id="img" src="./1.png" style="border: 1px solid gray"></img>
            </div>

            <label>Result:</label>
            <pre><code id="result"></code></pre>

            <p>See the <a href="https://github.com/zxing-js/library/tree/master/docs/examples/multi-image/">source code</a> for this example.</p>

        </section>

        <footer class="footer">
            <section class="container">
                <p>ZXing TypeScript Demo. Licensed under the <a target="_blank" href="https://github.com/zxing-js/library#license" title="MIT">MIT</a>.</p>
            </section>
        </footer>

    </main>

    <script type="text/javascript" src="https://unpkg.com/@zxing/library@latest"></script>
    <script type="text/javascript">
        window.addEventListener('load', function () {
            const codeReader = new ZXing.BrowserMultiFormatReader()
            console.log('ZXing code reader initialized')

            document.getElementById('decodeButton').addEventListener('click', () => {
                const img = document.getElementById('img')
                codeReader.decodeFromImage(img).then((result) => {
                    console.log(result)
                    document.getElementById('result').textContent = result.text
                }).catch((err) => {
                    console.error(err)
                    document.getElementById('result').textContent = err
                })
                console.log(`Started decode for image from ${img.src}`)
            })

        })
    </script>

</body>

</html>
```

上面是通过设置图片文件路径的方法
<img id="img" src="./1.png" style="border: 1px solid gray"></img>

或者修改为上传文件，选择本地文件：

```

<!doctype html> 
<html lang="zh-CN"> 
<head> 
    <meta charset="utf-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1"> 
    <meta name="author" content="ZXing for JS"> 
    <title>ZXing TypeScript | 从本地图像文件解码</title> 
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null"  href="https://fonts.googleapis.com/css?family=Roboto:300,300italic,700,700italic">  
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null"  href="https://unpkg.com/normalize.css@8.0.0/normalize.css">  
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null"  href="https://unpkg.com/milligram@1.3.0/dist/milligram.min.css">  
</head> 
<body> 
    <main class="wrapper" style="padding-top:2em"> 
        <section class="container" id="demo-content"> 
            <h1 class="title">从本地图像扫描一维/二维码</h1> 
            <p> 
                <a class="button-small button-outline" href="../../index.html"> 首页 🏡</a> 
            </p> 
            <p> 
                此示例展示如何使用ZXing JavaScript库从本地图像扫描任何支持的一维/二维码。 
                该示例将从用户选择的本地图像文件中进行解码。 
            </p> 
            <div> 
                <input type="file" id="imageFileInput" accept="image/*"> 
                <a class="button" id="decodeButton">解码</a> 
            </div> 
            <div id="imagePreview"> 
                <!-- 这里将动态显示选择的图像 --> 
            </div> 
            <label>结果:</label> 
            <pre><code id="result"></code></pre> 
            <p>查看此示例的 <a href="https://github.com/zxing-js/library/tree/master/docs/examples/multi-image/"> 源代码</a>.</p> 
        </section> 
        <footer class="footer"> 
            <section class="container"> 
                <p>ZXing TypeScript演示。遵循 <a target="_blank" href="https://github.com/zxing-js/library#license"  title="MIT">MIT许可协议</a>。</p> 
            </section> 
        </footer> 
    </main> 
    <script type="text/javascript" src="https://unpkg.com/@zxing/library@latest"></script>  
    <script type="text/javascript"> 
        window.addEventListener('load',  function () { 
            const codeReader = new ZXing.BrowserMultiFormatReader(); 
            console.log('ZXing 代码读取器已初始化'); 
 
            document.getElementById('decodeButton').addEventListener('click',  () => { 
                const fileInput = document.getElementById('imageFileInput');  
                const file = fileInput.files[0];  
                if (file) { 
                    const reader = new FileReader(); 
                    reader.onloadend  = () => { 
                        const img = new Image(); 
                        img.src  = reader.result;  
                        img.onload  = () => { 
                            codeReader.decodeFromImage(img).then((result)  => { 
                                console.log(result);  
                                document.getElementById('result').textContent  = result.text;  
                            }).catch((err) => { 
                                console.error(err);  
                                document.getElementById('result').textContent  = err; 
                            }); 
                            console.log(` 开始解码来自 ${file.name}  的图像`); 
                            // 显示图像预览 
                            const imagePreview = document.getElementById('imagePreview');  
                            imagePreview.innerHTML  = `<img src="${reader.result}"  style="border: 1px solid gray">`; 
                        }; 
                    }; 
                    if (file) { 
                        reader.readAsDataURL(file);  
                    } 
                } else { 
                    console.error(' 请选择一个图像文件'); 
                } 
            }); 
        }); 
    </script> 
</body> 
</html>
```

问copliot：
例子代码中打开摄像头的功能，这个是如何选择前后摄像头的。

下面是集成了从本地图像文件解码和从摄像头流解码，同时支持选择前后摄像头的完整HTML代码。这个代码将两个功能合并到了一个文件中，并且添加了选择前后摄像头的功能。

```
<!doctype html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="author" content="ZXing for JS">
    <title>ZXing TypeScript | 解码示例</title>
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null" href="https://fonts.googleapis.com/css?family=Roboto:300,300italic,700,700italic">
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null" href="https://unpkg.com/normalize.css@8.0.0/normalize.css">
    <link rel="stylesheet" rel="preload" as="style" onload="this.rel='stylesheet';this.onload=null" href="https://unpkg.com/milligram@1.3.0/dist/milligram.min.css">
</head>
<body>
    <main class="wrapper" style="padding-top:2em">
        <section class="container" id="demo-content">
            <h1 class="title">从本地图像或摄像头扫描一维/二维码</h1>
            <p>
                <a class="button-small button-outline" href="../../index.html">首页 🏡</a>
            </p>
            <p>此示例展示如何使用ZXing JavaScript库从本地图像文件或摄像头流扫描任何支持的一维/二维码。</p>
            
            <!-- 从本地图像解码 -->
            <div>
                <h2>从本地图像解码</h2>
                <input type="file" id="imageFileInput" accept="image/*">
                <a class="button" id="decodeButton">解码</a>
                <div id="imagePreview">
                    <!-- 这里将动态显示选择的图像 -->
                </div>
                <label>结果:</label>
                <pre><code id="resultImage"></code></pre>
            </div>
            
            <!-- 从摄像头流解码 -->
            <div>
                <h2>从摄像头流解码</h2>
                <div>
                    <a class="button" id="startButton">开始</a>
                    <a class="button" id="resetButton">重置</a>
                </div>
                <div>
                    <video id="video" width="300" height="200" style="border: 1px solid gray"></video>
                </div>
                <div id="sourceSelectPanel" style="display:none">
                    <label for="sourceSelect">更改视频源:</label>
                    <select id="sourceSelect" style="max-width:400px"></select>
                </div>
                <label>结果:结果只要打开摄像头，如果检测到就会实时显示</label>
                <pre><code id="resultCamera"></code></pre>
            </div>
            
            <p>查看此示例的 <a href="https://github.com/zxing-js/library/tree/master/docs/examples/multi-image/">源代码</a>.</p>
        </section>
        <footer class="footer">
            <section class="container">
                <p>ZXing TypeScript演示。遵循 <a target="_blank" href="https://github.com/zxing-js/library#license" title="MIT">MIT许可协议</a>。</p>
            </section>
        </footer>
    </main>
    <script type="text/javascript" src="https://unpkg.com/@zxing/library@latest"></script>
    <script type="text/javascript">
        window.addEventListener('load', function () {
            const codeReader = new ZXing.BrowserMultiFormatReader();
            console.log('ZXing 代码读取器已初始化');

            // 从本地图像解码
            document.getElementById('decodeButton').addEventListener('click', () => {
                const fileInput = document.getElementById('imageFileInput');
                const file = fileInput.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onloadend = () => {
                        const img = new Image();
                        img.src = reader.result;
                        img.onload = () => {
                            codeReader.decodeFromImage(img).then((result) => {
                                console.log(result);
                                document.getElementById('resultImage').textContent = result.text;
                            }).catch((err) => {
                                console.error(err);
                                document.getElementById('resultImage').textContent = err;
                            });
                            console.log(`开始解码来自 ${file.name} 的图像`);
                            // 显示图像预览
                            const imagePreview = document.getElementById('imagePreview');
                            imagePreview.innerHTML = `<img src="${reader.result}" style="border: 1px solid gray">`;
                        };
                    };
                    reader.readAsDataURL(file);
                } else {
                    console.error('请选择一个图像文件');
                }
            });

            // 从摄像头流解码
            let selectedDeviceId;
            codeReader.listVideoInputDevices()
                .then((videoInputDevices) => {
                    const sourceSelect = document.getElementById('sourceSelect');
                    selectedDeviceId = videoInputDevices[0].deviceId;
                    if (videoInputDevices.length >= 1) {
                        videoInputDevices.forEach((element) => {
                            const sourceOption = document.createElement('option');
                            sourceOption.text = element.label;
                            sourceOption.value = element.deviceId;
                            sourceSelect.appendChild(sourceOption);
                        });

                        sourceSelect.onchange = () => {
                            selectedDeviceId = sourceSelect.value;
                        };

                        const sourceSelectPanel = document.getElementById('sourceSelectPanel');
                        sourceSelectPanel.style.display = 'block';
                    }

                    document.getElementById('startButton').addEventListener('click', () => {
                        codeReader.decodeFromVideoDevice(selectedDeviceId, 'video', (result, err) => {
                            if (result) {
                                console.log(result);
                                document.getElementById('resultCamera').textContent = result.text;
                            }
                            if (err && !(err instanceof ZXing.NotFoundException)) {
                                console.error(err);
                                document.getElementById('resultCamera').textContent = err;
                            }
                        });
                        console.log(`Started continuous decode from camera with id ${selectedDeviceId}`);
                    });

                    document.getElementById('resetButton').addEventListener('click', () => {
                        codeReader.reset();
                        document.getElementById('resultCamera').textContent = '';
                        console.log('Reset.');
                    });

                })
                .catch((err) => {
                    console.error(err);
                });
        });
    </script>
</body>
</html>
```

https://github.com/zxing-js/library/tree/master/docs/examples/multi-camera/
例子代码中可以选择先后摄像头

```
                    <label for="sourceSelect">更改视频源:</label>
                    <select id="sourceSelect" style="max-width:400px"></select>
                </div>
                <label>结果:</label>
```

```
            // 从摄像头流解码
            let selectedDeviceId;
            codeReader.listVideoInputDevices()
                .then((videoInputDevices) => {
                    const sourceSelect = document.getElementById('sourceSelect');
                    selectedDeviceId = videoInputDevices[0].deviceId;
                    if (videoInputDevices.length >= 1) {
                        videoInputDevices.forEach((element) => {
                            const sourceOption = document.createElement('option');
                            sourceOption.text = element.label;
                            sourceOption.value = element.deviceId;
                            sourceSelect.appendChild(sourceOption);
                        });

```

这里是把俩摄像头，append进html的select id="sourceSelect" 中
 appendourceSelect.appendChild
 然后在html中，显示俩摄像头名为  camera2 1, facing front和camera2 2, facing back"

在juejin.cn代码中默认的是自拍摄像头，没法选择

```
                    // 默认获取第一个摄像头设备id
                    const firstDeviceId = videoInputDevices[0].deviceId; // 根据id选择摄像头
```
