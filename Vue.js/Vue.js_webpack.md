## webpack

### webpack이란?

- 서로 연관이 있는 모듈 간의 관계를 해석하여 정적인 자원으로 변환해 주는 도구이다.
- 애플리케이션을 이루는 여러개의 파일(HTML, CSS, Js, Image etc..)들을 1개의 자바스크립트 파일 안에 넣고, 자바스크립트 파일만 로딩해도 웹앱이 돌아가게 하는 것이다.

### 주요 속성

- entry : 웹팩으로 빌드할 대상 파일을 지정하는 속성. entry로 지정한 파일의 내용에는 전체 애플리케이션의 로직과 필요한 라이브러리를 로딩하는 로직이 들어간다.
- output : 웹팩으로 빌드한 결과물의 위치와 파일 이름 등 세부 옵션을 설정하는 속성이다.
- loader : 웹팩으로 빌드할 때 HTML, CSS, 이미지 파일 등을 자바스크립트로 변환하기 위해 필요한 설정을 정의하는 속성이다.
- plugin : 웹팩으로 빌드하고 나온 결과물에 대해 추가 기능을 제공하는 속성이다.(결과물의 사이즈를 줄이거나 기타 CSS, HTML파일로 분리하는 기능 등)
- resolve : 웹팩으로 빌드할 때 해당 파일이 어떻게 해석되는지 정의하는 속성이다.(특정 라이브러리를 로딩할 때 버전과 파일 경로를 정의한다)

### 웹팩 설정 파일

> Vue cli로 프로젝트를 생성하고 나면 프로젝트 내 최상위 레벨에서 webpack.config.js라는 웹팩 설정 파일이 생성된다. `npm run dev` 명령어를 입력했을 때 이 설정 파일에 따라 .vue파일을 포함한 기타 파일들이 웹팩으로 빌드된다.

1. 파일 경로와 웹팩 라이브러리 로딩

```js
const path = require("path");
const webpack = require("webpack");
```

> output 속성에서 사용할 노드 path 라이브러리와 웹팩 플러그인에서 사용할 node_modules의 웹팩 라이브러리를 node_modules 폴더에서 로딩하여 각 변수에 저장한다.  
> 2. entry 속성

```js
entry: {
			app: [
				'@babel/polyfill',
				path.join(__dirname,'main.js')
			]
		},
```

> 웹팩으로 빌드할 파일을 현재 파일 경로에 있는 main.js파일로 지정한다.  
> 3. output 속성

```js
output: {
			filename: 'app.js',
			path: path.join(__dirname, 'dist')
		},
```

> 빌드하고 난 결과물 파일의 위치와 이름을 지정한다.  
> 4. module 속성

```js
module: {
			rules: [
				// ... other rules
				{
					test: /\.vue$/,
					loader: 'vue-loader'
				},
				{
					test: /\.js$/,
					exclude: /node_modules/,
					loader: 'babel-loader'
				},
				// this will apply to both plain `.css` files
				// AND `<style>` blocks in `.vue` files
				{
					test: /\.css$/,
					use: [
					'vue-style-loader',
					'css-loader',
					'postcss-loader',
					]
				},
			]
		},
```

> 애플리케이션 파일들을 빌드할 때 HTML, CSS 등의 파일을 자바스크립트로 변환해 주는 로더를 지정한다.  
> 5. resolve 속성

```js
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    },
    extensions: ['*', '.js', '.vue', '.json']
  },
```

> 웹팩으로 빌드할 때 사용할 뷰 라이브러리 유형을 지정한다. vue.esm.js는 최신 웹팩 버전과 사용할 수 있는 풀 버전의 라이브러리를 의미한다. 별도로 설정하지 않으면 런타임 버전인 vue.runtime.sem.js를 사용한다.  
> 6. devServer 속성

```js
  devServer: {
    historyApiFallback: true,
    noInfo: true,
    overlay: true,
	hot: true
  },
```

> 웹팩 데브 서버 관련 속성을 지정한다.  
> `historyApiFallback` : 클라이언트 사이드 라우팅인 뷰 라우터와 함께 사용하기 위해 `true`로 지정한다.  
> `noInfo` : 처음 서버를 시작할 때만 빌드 정보를 보여주고, 이후 변경 시에는 빌드 정보를 보여주지 않는다.  
> `overlay` : 빌드할 때 오류가 있으면 브라우저 화면 전체에 오류를 표시한다.  
> `hot` : CSS 파일이나 Js파일을 변경하면 해당 모듈이 바로 업데이트 된다. 7. 배포 옵션

```js
if (process.env.NODE_ENV === "production") {
  module.exports.devtool = "#source-map";
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      "process.env": {
        NODE_ENV: '"production"',
      },
    }),
    new webpack.optimize.UglifyJsPlugin({
      sourceMap: true,
      compress: {
        warnings: false,
      },
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true,
    }),
  ]);
}
```

> 애플리케이션 기능과 화면을 구현한 후 최종적으로 사용자나 사이트에 배포할 때 설정하는 옵션이다.

### 웹팩 데브 서버 (webpack-dev-server)

> 웹팩 설정 파일(webpack.config.js)의 변화를 감지하여 빠르게 웹팩을 빌드할 수 있도록 지원하는 유틸리티이자 node.js서버

- `npm run build` 명령어로 /dist/라는 웹팩 빌드 결과물을 만들지 않아도 `npm run dev` 명령어를 실행했을 때 마치 웹팩으로 빌드한 것 같은 효과를 얻는다.
- 파일 시스템에 파일을 쓰고 읽는 시간보다 메모리에 저장하고 읽는 시간이 더 빠르기 때문이며 웹팩 데브 서버를 인 메모리 기반이라고 한다.
