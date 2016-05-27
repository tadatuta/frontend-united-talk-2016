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

## **BEM is not just about CSS**

## **Interfaces are built with <br> <span style="font-size: 200%">blocks</span>**

## **![](pictures/anatomy1.png)**
{:.cover}

## **![](pictures/anatomy2.png)**
{:.cover}

## **![](pictures/anatomy3.png)**
{:.cover}

## **![](pictures/anatomy4.png)**
{:.cover}

## **Blocks are made with <br> <span style="font-size: 200%">elements</span>**

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

## **Same blocks may behave differently with <span style="font-size: 200%">modifiers</span>**

## **![](pictures/cat_type_red.jpg)**
{:.cover}

## **![](pictures/cat_state_wet.jpg)**
{:.cover}

## **![](pictures/anatomy10.png)**
{:.cover}

## **![](pictures/anatomy11.png)**
{:.cover}

## Block Element Modifier
<div style="text-align: center; font-size: 146px">
    <img src="pictures/bem-method.svg" style="width: 600px"><br>

    <a style="color: #000; text-decoration: normal; top: -130px; display: inline-block; border: 0; background: 0; position: relative" href="https://en.bem.info/methodology/">bem.info</a>
</div>

## **CSS without conponent approach is <span style="font-size: 200%">pain</span>**

## **![](pictures/css.gif)**
{:.cover}

## **Blocks are <span style="font-size: 200%">independent</span> and <span style="font-size: 200%">self-contained</span>**

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
<button class="button"></button>
~~~

## BEMHTML: BEMJSON to HTML
~~~ markup
<font color="red">
    <button class="button"></button>
</font>
~~~

## BEMHTML: BEMJSON to HTML
~~~ markup
<button class="button"></button>
~~~

~~~css
.button {
    color: red;
}
~~~

## BEMHTML: BEMJSON to HTML
~~~ markup
<button class="button"></button>
<div>
    <button class="button"></button>
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
    block: 'button'
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
        block: 'button'
    },
    {
        content: {
            block: 'button'
        }
    }
]
~~~

~~~javascript
block('button')(
    tag()('button')
);
~~~

## **[BEMHTML](https://bem.github.io/bem-xjst/)**

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

## **Tune library on project side**

## Tune CSS

~~~python
library/
    button/
        button.css
~~~

## Tune CSS

~~~python
library/
    button/
        button.css

project/
    button/
        button.css
~~~

## Tune CSS

~~~python
library/
    button/
        button.css
            .button {
                width: 200px;
                color: green;
            }

project/
    button/
        button.css
~~~

## Tune CSS

~~~python
library/
    button/
        button.css
            .button {
                width: 200px;
                --color: green;--
            }

project/
    button/
        button.css
            .button {
                color: red;
            }
~~~

## Tune CSS

~~~python
library/
    button/
        button.css
            .button {
                width: 200px;
                --color: green;--
            }

project/
    button/
        button.css
            .button {
                color: red;
            }
~~~

~~~css
@import library/blocks/button/button.css;
@import project/blocks/button/button.css;
~~~

## Tune HTML
~~~python
library/
    button/
        button.bemhtml.js

project/
    button/
        button.bemhtml.js
~~~

## Tune HTML
~~~python
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

.button_disabled {
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

.button_disabled {
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

<footer>
    Под декларативностью здесь я подразумеваю такой способ описания поведения блоков, когда вы, как в CSS, задаете правила, кторые должны примениться к блоку в момент появления модификатора или при его снятии (когда на DOM-узле появляется/исчезает новый класс — стили с селектором на него автоматически применяются браузером).
</footer>

## **![](pictures/levels_en.png)**
{:.cover}

## **Ready-made UI libraries**

## **[![](pictures/bem-components-gh.png)](https://github.com/bem/bem-components/tree/v3/common.blocks)**
{:.cover}

## **[![](pictures/bem-components-showcase.png)](https://en.bem.info/libs/bem-components/)**
{:.cover}

## **Component based testing**

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

## **Let's take it all!**

## **[project-stub](https://github.com/bem/project-stub/)**

## **BEM is <span style="color: red;">not</span> just about CSS**

## **BEM is <span style="color: red;">not</span> just about CSS**
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

## **[bem.info](https://en.bem.info/)**


## **![](pictures/partially.png)**
{:.cover}


## **![](pictures/whole-platform.png)**
{:.cover}

## **Questions time!**

## **Contacts** {#contacts}

<div class="info">
<p class="author">{{ site.author.name }}</p>
<br>
<!-- <p class="position">{{ site.author.position }}</p> -->

    <div class="contacts">
        <p class="contacts-left contacts-top">bem.info</p>
        <p class="contacts-left mail">info@bem.info</p>
        <p class="contacts-right twitter">bem_en&nbsp;&nbsp;&nbsp;&nbsp;#b_</p>
        <!-- <p class="contacts-right contacts-bottom vk">vk</p>
        <p class="contacts-right facebook">facebook</p> -->
    </div>
    <div class="slides-link" style="font-size: 200%"><a href="http://tadatuta.github.io/frontend-united-talk-2016/">tadatuta.github.io/frontend-united-talk-2016</a></div>
</div>
