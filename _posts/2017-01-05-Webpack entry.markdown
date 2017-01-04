---
layout: post
title: "백엔드 잡부 프론트 도전 - Webpack Entry"
subtitle: "Webpack Entry"
date: 2017-01-05
author: bluemirr5
category: dev/Webpack
tags: webpack frontend
finished: true
comments: true
---

## Entry
Entry는 웹팩 설정에서 'entry'라는 프로퍼티로 정의하는데 여러가지 방식으로 정의할수 있다.

### 1. 단일 프로퍼티 : `entry: string|Array<string>`
{% highlight javascript %}
module.exports = {
    entry: './src/app.js',
    output: {
        filename: 'result.js',
        path: './dist'
    }
};
{% endhighlight %}
`app.js`단일 엔트리가 해당 의존성을 포함하여 번들링되어 `result.js`가 나오게 된다.

{% highlight javascript %}
module.exports = {
    entry: ['./src/app.js', './src/app2.js'],
    output: {
        filename: 'result.js',
        path: './dist'
    }
};
{% endhighlight %}
`app.js`와 `app2.js`의 의존 모듈들이 합하여져서 result.js로 번들링 된다.
<hr />
### 2. 객체 선언 : `entry: {[entryChunkName: string]: string|Array<string>}`
{% highlight javascript %}
module.exports = {
    entry: {
        app: './src/app.js'
    },
    output: {
        filename: 'result.js',
        path: './dist'
    }
};
{% endhighlight %}
`app.js`단일 엔트리가 해당 의존성을 포함하여 번들링되어 'result.js'가 나오게 된다.

{% highlight javascript %}
module.exports = {
    entry: {
        app: './src/app.js',
        app2: './src/app2.js'
    },
    output: {
        filename: 'result.js',
        path: './dist'
    }
};
{% endhighlight %}
위와 같이 다른 프로퍼티(app, app2)로 정의하고 output을 단일로 주게 되면 나중에 정의된 app2 엔트리만 번들링되어 'result.js'가 나오게 된다.
서로 각각 다른 멀티 아웃풋을 원한다면 아래와 같이 정의한다.

{% highlight javascript %}
module.exports = {
    entry: {
        app: './src/app.js',
        app2: './src/app2.js'
    },
    output: {
        filename: '[name].js',
        path: './dist'
    }
};
{% endhighlight %}
output을 '[name].js'와 같이 정의하면 변수 처리되어 'app.js'와 'app2.js' 파일이 의존성을 포함하여 번들링되어 나오게 된다.
<hr />
