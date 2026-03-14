如何开发自己的插件呢？

 - 目前大部分插件都可以在社区中找到，但是推荐尽量使用在维护，并且经过社区验证的；
 - 这里我们开发一个自己的插件：**将静态文件自动上传服务器中**；

自定义插件的过程：

 - 创建AutoUploadWebpackPlugin类；
 - 编写apply方法：
	 - 通过ssh连接服务器；
	 - 删除服务器原来的文件夹；
	 - 上传文件夹中的内容；
 - 在webpack的plugins中，使用AutoUploadWebpackPlugin类；

代码中和服务器连接需要使用到 node-ssh:

```shell
npm install node-ssh -D
```


插件代码：

```js
// AutoUploadWebpackPlugin.js
const { NodeSSH } = require("node-ssh");

class AutoUploadWebpackPlugin {
  constructor(options) {
    this.ssh = new NodeSSH();
    this.options = options;
  }
  apply(compiler) {
    // 等到assets已经输出到output目录上时，·完成自动上传的功能
    compiler.hooks.afterEmit.tapAsync(
      "AuotPlugin",
      async (compilation, callback) => {
        // 获取输出文件夹路径(静态资源)
        const outputPath = compilation.outputOptions.path;
        console.log(outputPath);

        // 使用ssh连接服务器
        await this.connectServer();
        // 删除原有文件夹里面的所有内容
        const remotePath = this.options.remotePath;
        await this.ssh.execCommand(`rm -rf ${remotePath}/*`);

        // 使用sftp将静态资源上传到服务器上
        await this.uploadFiles(outputPath, remotePath);

        // 关闭和服务器的连接
        this.ssh.dispose();

        // 完成所有操作后，调用callback
        callback();
      },
    );
  }

  async connectServer() {
    //  使用SSH连接到远程服务器
    await this.ssh.connect({
      host: this.options.host,
      port: this.options.port,
      username: this.options.username,
      password: this.options.password,
    });
  }

  async uploadFiles(localPath, remotePath) {
    //  通过SSH连接将本地目录上传到远程服务器 使用putDirectory方法执行目录上传操作
    const status = await this.ssh.putDirectory(localPath, remotePath, {
      recursive: true, //  递归上传目录及其子目录
      concurrency: 10, //  设置并发上传的文件数量为10
    });
    if (status) {
      console.log("文件上传成功");
    }
  }
}

//  导出AutoUploadWebpackPlugin类，使其可以被其他模块引用
module.exports = AutoUploadWebpackPlugin;
//  同时以属性方式导出AutoUploadWebpackPlugin，提供另一种引用方式
module.exports.AutoUploadWebpackPlugin = AutoUploadWebpackPlugin;

```


```js
// webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const AutoUploadWebpackPlugin = require("./plugins/AutoUploadWebpackPlugin")

module.exports = {
  mode: "development",
  entry: "./src/main.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "./build"),
  },
  plugins: [
    new HtmlWebpackPlugin(),
    new AutoUploadWebpackPlugin({
      host: "localhost",
      port: 8080,
      username: "axl",
      password: "123456",
      remotePath: "root/test/"
    })
  ],
};

```


