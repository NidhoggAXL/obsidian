
如果我们项目中需要处理css文件，可以使用postcss：

```shell
npm install rollup-plguin-postcss postcss -D
# 如需自动添加前缀，再安装 autoprefixer
npm install autoprefixer -D
```

配置postcss的插件：

```js
// rollup.config.js
import postcss from 'rollup-plugin-postcss';
import autoprefixer from 'autoprefixer'; // 可选

export default {
  input: 'src/index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'iife' // 或 'es', 'cjs' 等
  },
  plugins: [
    postcss({
      // 提取 CSS 到单独文件（默认内联在 JS 中）
      extract: true,           // 生成 dist/bundle.css
      // 或指定文件名：extract: 'dist/styles.css'

      // 开启 CSS Modules（默认关闭）
      // modules: true,

      // 使用 PostCSS 插件（如 autoprefixer）
      plugins: [autoprefixer()],

      // 支持预处理器（需额外安装 node-sass 等）
      // use: ['sass'],

      // 是否压缩（生产环境可开启）
      // minimize: true,
    })
  ]
};
```

