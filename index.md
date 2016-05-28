---

layout: default

---

# BEM

## **{{ site.presentation.title }}** {#cover}

<div class="s">
    <div class="service">{{ site.presentation.service }}</div>
</div>

{% if site.presentation.nda %}
<div class="nda"></div>
{% endif %}

<div class="info">
	<p class="author">{{ site.author.name }}, <br/> {{ site.author.position }}</p>
</div>

## **<span style="font-size: 150%">BEM is <span style="color: red">not</span> just about CSS</span>**

## **Interfaces are built with <br> <span style="font-size: 200%; line-height: 1.6">blocks</span>**

## **![](pictures/anatomy1.png)**
{:.cover}

## **![](pictures/anatomy2.png)**
{:.cover}

## **![](pictures/anatomy3.png)**
{:.cover}

## **![](pictures/anatomy4.png)**
{:.cover}

## **Blocks are made of <br> <span style="font-size: 200%; line-height: 1.6">elements</span>**

## **![](pictures/anatomy5.png)**
{:.cover}

## **![](pictures/anatomy6.png)**
{:.cover}

## **![](pictures/anatomy7.png)**
{:.cover}

## **![](pictures/anatomy8.png)**
{:.cover}

## **![](pictures/anatomy9.png)**
{:.cover}

## **Same blocks may behave differently with <span style="font-size: 200%; line-height: 1.6">modifiers</span>**

## **![](pictures/cat_type_red.jpg)**
{:.cover}

## **![](pictures/cat_state_wet.jpg)**
{:.cover}

## **![](pictures/anatomy10.png)**
{:.cover}

## **![](pictures/anatomy11.png)**
{:.cover}

## <span></span>
<div style="text-align: center; font-size: 146px">
    <img src="pictures/bem-method.svg" style="width: 600px"><br>

    <a style="color: #000; text-decoration: normal; top: -130px; display: inline-block; border: 0; background: 0; position: relative" href="https://en.bem.info/methodology/">bem.info</a>
</div>

## **CSS without component approach is <br> <span style="font-size: 200%; line-height: 1.6">a pain</span>**

## **![](pictures/css.gif)**
{:.cover}

## **Blocks are <br> <span style="font-size: 200%; line-height: 1.3">independent</span> <br> and <br> <span style="font-size: 200%;  line-height: 1.3">self-contained</span>**

## **![](pictures/yog.svg)**
{:.cover}

## BEM on file system

~~~ python
blocks/
    button/
        button.css
        button.js
~~~

## BEM on file system

~~~ python
blocks/
    button/
        button.css
        button.js
        button.spec.js
~~~

## BEM on file system

~~~ python
blocks/
    button/
        button.css
        button.js
        button.spec.js
        button.md
~~~

## BEM tree

~~~ markup
<body class="page">
    <header class="header">
        <a class="logo" href="/"></a>
    </header>

    <div class="main"></div>

    <aside class="sidebar"></aside>

    <footer class="footer">
        <div class="copyright"></div>
    </footer>
</body>
~~~

<footer>
HTML maps to DOM tree
We need a way to describe interfaces in Blocks Elements and Modifiers
</footer>

## BEM tree

~~~ python
page
    header
        logo
    main
    sidebar
    footer
        copyright
~~~

## BEMJSON

~~~javascript
{
    block: 'page',
    title: 'Hello, BEM',
    content: [
        {
            block: 'header',
            content: { block: 'logo' }
        },
        { block: 'main' },
        { block: 'sidebar' },
        {
            block: 'footer',
            content: { block: 'copyright' }
        }
    ]
}
~~~

## Mixes: several entities on same node

~~~ markup
<nav class="nav">
    <a class="link nav__item" href="/">Main</a>
    <a class="link nav__item" href="/about/">About</a>
</nav>
~~~

## Mixes: several entities on same node

~~~ javascript
{
    block: 'nav',
    content: [
        {
            block: 'link',
            url: '/',
            mix: { block: 'nav', elem: 'item' },
            content: 'Main'
        },
        {
            block: 'link',
            url: '/about/',
            mix: { block: 'nav', elem: 'item' },
            content: 'About'
        }
    ]
}
~~~

## BEMHTML: BEMJSON to HTML
~~~ markup
<button class="button">I'm a button</button>
~~~

## BEMHTML: BEMJSON to HTML
~~~ markup
<button class="button">
    <font color="red">I'm a button</font>
</button>
~~~

## BEMHTML: BEMJSON to HTML
~~~ markup
<button class="button">I'm a button</button>
~~~

~~~css
.button {
    color: red;
}
~~~

## BEMHTML: BEMJSON to HTML
~~~ markup
<button class="button">I'm a button</button>
<div>
    <button class="button">I'm another button</button>
</div>
~~~

~~~css
.button {
    color: red;
}
~~~

## BEMHTML: BEMJSON to HTML

~~~javascript
{
    block: 'button',
    content: 'I am button'
}
~~~

~~~javascript
block('button')(
    tag()('button')
);
~~~

## BEMHTML: BEMJSON to HTML

~~~javascript
[
    {
        block: 'button',
        content: 'I am button'
    },
    {
        content: {
            block: 'button',
            content: 'I am another button'
        }
    }
]
~~~

~~~javascript
block('button')(
    tag()('button')
);
~~~

## **<span style="font-size: 250%; letter-spacing: 5px">[BEMHTML](https://bem.github.io/bem-xjst/)</span>**

## BEM on file system

~~~python
blocks/
    button/
        button.css
        button.js
        button.spec.js
        button.md
~~~

## BEM on file system

~~~python
blocks/
    button/
        button.css
        button.js
        button.spec.js
        button.md
        button.bemhtml.js
~~~

## **![](pictures/good.gif)**
{:.cover}

## **<span style="font-size: 140%">Tune library on project side</span>**

## Tune CSS

~~~python
library/button/button.css
~~~

## Tune CSS

~~~python
library/button/button.css
~~~

~~~python
project/button/button.css
~~~

## Tune CSS

~~~python
library/button/button.css
~~~
~~~css
    .button {
        width: 200px;
        color: green;
    }
~~~
~~~python
project/button/button.css
~~~

## Tune CSS

~~~python
library/button/button.css
~~~
~~~css
    .button {
        width: 200px;
        --color: green;--
    }
~~~
~~~python
project/button/button.css
~~~
~~~css
    .button {
        color: red;
    }
~~~

## Tune CSS

~~~python
library/button/button.css
~~~
~~~css
    .button {
        width: 200px;
        --color: green;--
    }
~~~
~~~python
project/button/button.css
~~~
~~~css
    .button {
        color: red;
    }
~~~

~~~css
@import library/blocks/button/button.css;
@import project/blocks/button/button.css;
~~~

## Tune HTML
~~~javascript
library/
    button/
        button.bemhtml.js

project/
    button/
        button.bemhtml.js
~~~

## Tune HTML
~~~javascript
library/
    button/
        button.bemhtml.js

            block('button')(
                tag()('button'),
                attrs()({ 'area-role': 'button' })
            );

project/
    button/
        button.bemhtml.js

            block('button')(
                tag()('input')
            );
~~~

## Tune JavaScript
~~~ css
.button {
    border-radius: 5px;
}

.button--disabled {
    opacity: .5;
}
~~~

~~~markup
<button class="button"></button>
~~~

## Tune JavaScript
~~~ css
.button {
    border-radius: 5px;
}

.button--disabled {
    opacity: .5;
}
~~~

~~~markup
<button class="button button_disabled"></button>
~~~

## Tune JavaScript
~~~ javascript
BEMDOM.decl('button', {








});
~~~

## Tune JavaScript

~~~ javascript
BEMDOM.decl('button', {
    onSetMod: {




    }


});
~~~

## Tune JavaScript

~~~ javascript
BEMDOM.decl('button', {
    onSetMod: {
        disabled: {


        }
    }


});
~~~

## Tune JavaScript

~~~ javascript
BEMDOM.decl('button', {
    onSetMod: {
        disabled: {
            true: { this._onDisabled(); }

        }
    },
    _onDisabled: function() {}

});
~~~

## Tune JavaScript

~~~ javascript
BEMDOM.decl('button', {
    onSetMod: {
        disabled: {
            true: { this._onDisabled(); },
            '': { this._onEnabled(); }
        }
    },
    _onDisabled: function() {},
    _onEnabled: function() {}
});
~~~

## **![](pictures/levels_en.png)**
{:.cover}

## **![](pictures/horse.gif)**
{:.cover}

## **<span style="font-size: 140%">Ready-made UI libraries</span>**

## **[![](pictures/bem-components-gh.png)](https://github.com/bem/bem-components/tree/v3/common.blocks)**
{:.cover}

## **[![](pictures/bem-components-showcase.png)](https://en.bem.info/libs/bem-components/)**
{:.cover}

## **<span style="font-size: 140%">Component based testing</span>**

## **[![](pictures/travis1.png)](https://travis-ci.org/bem/bem-components)**
{:.cover}

## **[![](pictures/travis2.png)](https://travis-ci.org/bem/bem-components)**
{:.cover}

## **[![](pictures/travis3.png)](https://travis-ci.org/bem/bem-components)**
{:.cover}

## **[![](pictures/travis4.png)](https://travis-ci.org/bem/bem-components)**
{:.cover}

## **[![](pictures/travis5.png)](https://travis-ci.org/bem/bem-components)**
{:.cover}

## **<span style="font-size: 200%">Let's take it all!</span>**

## **![](pictures/tools.gif)**
{:.cover}

## **[<span style="font-size: 250%">project-stub</span>](https://github.com/bem/project-stub/)**

## **<span style="font-size: 130%">BEM is <span style="color: red">not</span> just about CSS</span>**

## **<span style="font-size: 130%">BEM is <span style="color: red;">not</span> just about CSS</span>**
<div class="stump"></div>

## BEM is not just about CSS

* Component approach to build interfaces
* ...Declarative JS
* ...Declarative templates
* ...Great libraries with ready-made blocks
* ...Sofisticated build system
* ...Tools to work with blocks on FS
* ...SDK to build your own tools
* ...and more

## **[<span style="font-size: 300%">bem.info</span>](https://en.bem.info/)**


## **![](pictures/partially.png)**
{:.cover}


## **![](pictures/whole-platform.png)**
{:.cover}

## **![](pictures/questions.gif)**
{:.cover}

## **Contacts** {#contacts}

<div class="info" style="margin-top: 100px">
<p class="author" style="font-size: 50px">{{ site.author.name }}</p>
<br>
<!-- <p class="position">{{ site.author.position }}</p> -->

    <div class="contacts">
        <p class="contacts-left contacts-top" style="font-size: 50px !important">bem.info</p>
        <p class="contacts-left mail" style="font-size: 50px !important">info@bem.info</p>
        <p class="contacts-right twitter" style="font-size: 50px !important">bem_en&nbsp;&nbsp;&nbsp;&nbsp;#b_</p>
        <!-- <p class="contacts-right contacts-bottom vk">vk</p>
        <p class="contacts-right facebook">facebook</p> -->
    </div>
    <div class="slides-link" style="font-size: 300%"><a href="http://tadatuta.github.io/frontend-united-talk-2016/">tadatuta.github.io/frontend-united-talk-2016</a></div>
</div>
