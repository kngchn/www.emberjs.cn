## Customizing a View's Element

## 自定义视图元素

A view is represented by a single DOM element on the page. You can change what kind of element is created by
changing the `tagName` property.

视图在页面上表现为一个单一的DOM元素。通过修改`tagName`属性，可以改变视图生成的元素的类型。

```javascript
App.MyView = Ember.View.extend({
  tagName: 'span'
});
```

You can also specify which class names are applied to the view by setting its `classNames` property to an array of strings:

另外，还可以通过设置一个字符串数组到`classNames`属性，来设置视图要应用的样式列表。

```javascript
App.MyView = Ember.View.extend({
  classNames: ['my-view']
});
```

If you want class names to be determined by the state of properties on the view, you can use class name bindings. If you bind to
a Boolean property, the class name will be added or removed depending on the value:

如果需要通过视图的属性来决定使用什么样式，那么可以采用样式名绑定。如果绑定了一个布尔属性，那么是否应用样式则有该属性的值来决定：

```javascript
App.MyView = Ember.View.extend({
  classNameBindings: ['isUrgent'],
  isUrgent: true
});
```

This would render a view like this:

上述的代码将会把视图渲染为：

```html
<div class="ember-view is-urgent">
```

If isUrgent is changed to false, then the `is-urgent` class name will be removed.

如果`isUrgent`变为`false`，那么`is-urgent`样式将被删除。

By default, the name of the Boolean property is dasherized. You can customize the class name
applied by delimiting it with a colon:

默认情况下，布尔属性的名称会采用中划线分割的方式命名。通过使用分号来定界，可以自定义样式的名称。

```javascript
App.MyView = Ember.View.extend({
  classNameBindings: ['isUrgent:urgent'],
  isUrgent: true
});
```

This would render this HTML:

上述代码将渲染出如下的HTML：

```html
<div class="ember-view urgent">
```

Besides the custom class name for the value being `true`, you can also specify a class name which is used when the value is `false`:

不仅可以在属性值为`true`的时候自定义样式名，同样也可以指定属性值为`false`的时候使用的样式名：

```javascript
App.MyView = Ember.View.extend({
  classNameBindings: ['isEnabled:enabled:disabled'],
  isEnabled: false
});
```

This would render this HTML:

上述代码将渲染出如下的HTML：

```html
<div class="ember-view disabled">
```

You can also specify to only add a class when the property is `false` by declaring `classNameBindings` like this:

另外，通过按照如下的方式声明`classNameBindings`，来指定只在属性为`false`的要使用的样式：

```javascript
App.MyView = Ember.View.extend({
  classNameBindings: ['isEnabled::disabled'],
  isEnabled: false
});
```

This would render this HTML:

上述代码将渲染出如下的HTML：

```html
<div class="ember-view disabled">
```

If the `isEnabled` property is set to `true`, no class name is added:

如果`isEnabled`属性被设置为`true`，那么不会添加任何样式：

```html
<div class="ember-view">
```

If the bound value is a string, that value will be added as a class name without
modification:

如果绑定的值是字符串，那么该值会直接作为样式名添加到视图：

```javascript
App.MyView = Ember.View.extend({
  classNameBindings: ['priority'],
  priority: 'highestPriority'
});
```

This would render this HTML:

上述代码将渲染出如下的HTML：

```html
<div class="ember-view highestPriority">
```

#### Attribute Bindings on a View

#### 视图属性绑定

You can bind attributes to the DOM element that represents a view by using `attributeBindings`:

通过`attributeBindings`可以直接绑定代表视图的DOM元素的属性：

```javascript
App.MyView = Ember.View.extend({
  tagName: 'a',
  attributeBindings: ['href'],
  href: "http://emberjs.com"
});
```

You can also bind these attributes to differently named properties:

也可以将这些属性绑定到其他命名的属性上：

```javascript
App.MyView = Ember.View.extend({
  tagName: 'a',
  attributeBindings: ['customHref:href'],
  customHref: "http://emberjs.com"
});
```

### Customizing a View's Element from Handlebars

### 在Handlebars中自定义视图元素

When you append a view, it creates a new HTML element that holds its content.
If your view has any child views, they will also be displayed as child nodes
of the parent's HTML element.

当追加一个视图的时候，其创建了一个新的HTML元素来存放其内容。如果视图含有子视图，子视图将作为父视图HTML元素的子节点来显示。

By default, new instances of `Ember.View` create a `<div>` element. You can
override this by passing a `tagName` parameter:

默认情况下，`Ember.View`的实例创建一个`<div>`元素。通过传入一个`tagName`参数可以覆盖这个默认行为：

```handlebars
{{view App.InfoView tagName="span"}}
```

You can also assign an ID attribute to the view's HTML element by passing an `id` parameter:

同样传入`id`参数可以指定视图HTML元素的ID属性：

```handlebars
{{view App.InfoView id="info-view"}}
```

This makes it easy to style using CSS ID selectors:

这使得可以容易的采用CSS ID选择器来定义样式：

```css
/** Give the view a red background. **/
#info-view {
  background-color: red;
}
```

You can assign class names similarly:

样式名称也可以采用类似的方式来指定：

```handlebars
{{view App.InfoView class="info urgent"}}
```

You can bind class names to a property of the view by using `classBinding` instead of `class`. The same behavior as described in `bind-attr` applies:

采用`classBinding`而不是`class`可以将样式名绑定到视图的一个属性。这与`bind-attr`的行为一致：

```javascript
App.AlertView = Ember.View.extend({
  priority: "p4",
  isUrgent: true
});
```

```handlebars
{{view App.AlertView classBinding="isUrgent priority"}}
```

This yields a view wrapper that will look something like this:

上述代码生成如下的视图包裹：

```html
<div id="ember420" class="ember-view is-urgent p4"></div>
```
