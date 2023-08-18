# yang-css

## 解决什么问题？
* 提供一些常用的纯 CSS 组件
* 提供一些常用的 CSS 布局
* 提供一些常用的 CSS 工具（Mixins）函数

## 使用方式
1. 在 Webpack 中使用

```js
module.exports = {
    // webpack.config.js
    module: {
        rules: [
            {
                test: /\.scss$/,
                use: [
                    'style-loader',
                    {
                        loader: 'sass-loader',
                        options: {
                            data: `@import "node_modules/yang-css/scss/mixin.scss";`
                        }
                    }
                ]
            },
            {
                test: /\.less$/,
                use: [
                    'style-loader',
                    {
                        loader: 'less-loader',
                        options: {
                            data: `@import "node_modules/yang-css/less/mixin.less";`
                        }
                    }
                ]
            }
        ]
    }
}
```

2. 在 Vite 中使用

```js
// vite.config.js
export default defineConfig({
    ...,
	css: {
		preprocessorOptions: {
			scss: {
				additionalData: `@import "node_modules/yang-css/scss/mixin.scss";`
			},
			less: {
				additionalData: `@import "node_modules/yang-css/less/mixin.less";`
			}
		}
	},
    ...
})
```

3. 在 craco 中使用
```js
const sassResourcesLoader = require('craco-sass-resources-loader');
module.exports = {
    plugins: [
      {
        plugin: sassResourcesLoader,
        options: {
          resources: [
            'node_modules/yang-css/scss/mixin.scss',
          ],
        },
      },
    ],
};

const CracoLessPlugin = require('craco-less');
module.exports = {
    plugins: [
      {
        plugin: CracoLessPlugin,
        options: {
          lessLoaderOptions: {
            lessOptions: {
              modifyVars: {
                '@error-color': '#1890ff'
              },
              javascriptEnabled: true,
            },
            additionalData: `@import "node_modules/yang-css/less/mixin.less";`
          }
        },
      }
    ],
};
```