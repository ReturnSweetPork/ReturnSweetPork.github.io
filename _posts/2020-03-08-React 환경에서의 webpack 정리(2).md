# React 환경에서의 webpack 정리(2)

react 개발을 진행하면서 웹팩에 대한 개념을 정리하고 이를 통해서 손쉽게 웹팩을 다룰수 있도록 목표를 갖고 작성하였습니다.

## 웹팩에서 css 사용하기

```
//src/style.css를 만들기

.title {
color: #2196f3;
font-size:52px;
text-align:center;
}
```

```
//src/Root.js 에서 style.css 를 가져올수 있도록 import 진행

import React from 'react';
import './style.css';
const Root = () => {
  return <h3>Hello, React</h3>;
};

export default Root;
```

- 그후 yarn build 명령어로 빌드를 진행할 경우 file을 읽을수 없다고 나온다.

![image-20200309100257101](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200309100257101.png)



- 그 이유는 css-loader가 없기때문이다 -> css loader 적용을 통해서 css를 읽을수 있게 해준다.

```
//webpack.config.js에 css-loader를 추가해 줌.
      {
        test: /\.css$/,
        use: ['css-loader'],
      },
```

- 그후 yarn build를 진행하면 정상적으로 build는 되나 css가 적용 되지 않는다.
- 그 이유는 웹팩에서 css 파일을 읽은후 어딘가에 저장을 해야하기 때문이다.
- 2가지 방법이 존재함.
  - index.html 파일에 css를 합치는 방법(index에서 직접 css 선언)
  - 파일을 추출하여 따로 저장(webpack.config에서 css 추출하는 플러그인 적용)

```
//webpack.config.js에 css추출후 파일로 저장하는 플러그인 추가.
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build")
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ['babel-loader'],
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader']
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: './public/index.html', // public/index.html 파일을 읽는다.
      filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
    }),
    new MiniCssExtractPlugin({
      filename: 'style.css'
    })
  ]
};

```

- 아래와 같이 css가 적용된다.
- ![image-20200309101111339](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200309101111339.png)

## 웹팩에서 scss 사용하기

```
//src/style.scss 파일을 만들어 추가.

$fontColor: #2196f3;
$fontSize: 52px;


.title {
  color: $fontColor;
  font-size: $fontSize;
  text-align: center;
}
```

```
//src/Root.js 에 scss 를 import 진행

import React from 'react';
import './style.scss';
const Root = () => {
  return <h3 className="title">Hello, React</h3>;
};

export default Root;

```

- 빌드시, css와 동일하게  에러가 발생.
- scss 파일을 읽을수 없기에 에러가 나옴 -> 웹팩이 scss 파일을 읽을수 있도록 해줘야 함.

```
//webpack.config.js에 scss loader를 추가한다.

    {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
      }
```

## 웹팩에서 개발서버 적용하기

- 수정할때마다 웹팩 빌드를 이용하면 시간적으로 많이 불편
- 소스코드를 수정할때마다 알아서 웹팩이 빌드해주는 webpack-dev-server 적용

```
//webpack.config.js 파일에 들어가 devServer를 추가
  devServer: {
    contentBase: path.resolve("./build"),
    index: "index.html",
    port: 9000
  },
  
  //package.json 파일에 들어가 script 에 yarn start 추가
 "scripts": {
	"build": "webpack",
	"start": "webpack-dev-server --hot"
} 
  

```

![image-20200309111542421](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200309111542421.png)

- 수정사항이 발생한 경우 자동으로 빌드해주는 것을 확인할수 있다.

## 빌드 디렉터리 깨끗하게 하기

- clean-webpack-plugin을 통해서 빌드될때마다 안쓰는 파일들을 삭제할수 있도록 함.

```
//webpack.config.js
//plugin에 MiniCssExtractPlugin에 filename을 style-test.css로 변경

plugins: [
	new HtmlWebPackPlugin({
		template: './public/index.html', // public/index.html 파일을 읽는다.
		filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
	}),
	new MiniCssExtractPlugin({
		filename: 'style-test.css'
	})
]

```

- yarn build 명령어 후 안쓰는 style.css가 계속 남아있는것을 볼수 있음.
- clean-webpack-plugin 을 사용하여 안쓰는 build 파일을 자동으로 삭제

```
 //webpack.config.js
 
const {CleanWebpackPlugin} = require("clean-webpack-plugin");
 
 plugins: [
    new HtmlWebPackPlugin({
      template: './public/index.html', // public/index.html 파일을 읽는다.
      filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
    }),
    new MiniCssExtractPlugin({
      filename: 'style-test.css'
    }),
    new CleanWebpackPlugin()
  ]
```

- 결과적으로 웹팩 빌드후 style.css가 자동삭제되는 것을 볼수 있다.

## 웹팩 빌드 모드 나누기

- 웹팩의 빌드 모드는 development, production, none
- development는 빠르게 빌드하기 위해서 빌드할때 최적화를 하지 않는다.
- production은 빌드할때 최적화 작업을 진행한다.
- none은 아무것도 하지 않는다.
- config 디렉토리에 webpack.config.dev.js 와 webpack.config.pod.js를 나누어 생성

```javascript
//webpack.config.dev.js

const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const {CleanWebpackPlugin} = require("clean-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "../build")
  },
  mode: "development",
  devServer: {
    contentBase: path.resolve(__dirname, "../build"),
    index: "index.html",
    port: 9000
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ["babel-loader"]
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"]
      },
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html",
      filename: "index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "style.css"
    }),
    new CleanWebpackPlugin()
  ]
};


//config/webpack.config.prod.js

const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const {CleanWebpackPlugin} = require("clean-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.[contenthash].js",
    path: path.resolve(__dirname, "../build")
  },
  mode: "production",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ["babel-loader"]
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"]
      },
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html",
      filename: "index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "style.css"
    }),
    new CleanWebpackPlugin()
  ]
};

```

- 현재 코드상의 차이는 mode 값의 production 과 development 차이이다.
- 하지만 dev 와 prod에 맞는 플러그인들을 적용하며 붙여가기 시작할 경우에 mode에 따른 강점이 생김

```
//package.json

"scripts": {
  "start": "webpack-dev-server --config ./config/webpack.config.dev --hot",
  "build": "webpack --config ./config/webpack.config.prod"
 },
```

## 마무리

실제로 웹팩을 사용하면서 설정을 몇개 안한것 같았는데 생각보다 로더가 너무 다양해서 매우 놀랐다.

개인적으로는 추가로 웹팩을 통해서 모듈 분리를 진행하는 방법을 추가로 공부해야 겠다는 생각을 하게 되었다.



마지막으로 이 웹팩 개념을 통해서 지금 진행하는 프로젝트의 웹팩 설정부터 조금 수정해야겠다..!!