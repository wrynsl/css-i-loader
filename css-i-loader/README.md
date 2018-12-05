# css-i-loader

---
base on css-loader@0.28.7
---

## new css module

*case

```
p {
    color: red;
}
```

compile to

```
p._2T3cb522lYTcMXtTPySLFE {
    color: red;
}
```
---

```
p:global a {
    color: red;
}
```
compile to

```
p._2T3cb522lYTcMXtTPySLFE a{
    color: red;
}
```
---

```
:global p a {
    color: red;
}
```
compile to

```
p a {
    color: red;
}
```

## Usage

add a new api classModule ( default false) base css-loader,
when classModule is true, camelCase and modules are invalid

>getLocalIdent: function(loaderContext, localIdentName, filepath, options) {}
if getLocalIdent dont return a value, the file(filepath) do not be scoped;


in js demo：

app.css
```
	.app {
		color: red
	}
	.app p {
		color: blue
	}
```

compile to
```
	.app._3Be5_9HpSBoUhun9UFwgDE {
		color: red
	}
	.app p._3Be5_9HpSBoUhun9UFwgDE {
		color: blue
	}
```

app.jsx

```
import React from 'react';
import scopedClass from './app.css'; // scopedClass is _3Be5_9HpSBoUhun9UFwgDE

export default function App() {
	return <div className={`app ${scopedClass}`}><p className={scopedClass}>xxx</p></div>
}
```