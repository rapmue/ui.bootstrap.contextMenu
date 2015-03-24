#contextMenu

AngularJS UI Bootstrap Module for adding context menus to elements. [Demo](http://jsfiddle.net/ykbjd90z/1/)

`bower install angular-bootstrap-contextmenu`

[![Example](http://templarian.com/files/angularjs_contextmenu.png)](http://jsfiddle.net/ykbjd90z/1/)

## Usage

Add a reference to `contextMenu.js`. In your app config add `ui.bootstrap.contextMenu` as a dependency module.

### View

```html
<div>
    <div ng-repeat="item in items" context-menu="menuOptions">Right Click: {{item.name}}</div>
</div>
<div ng-bind="selected"></div>
```

### Controller

```js
$scope.selected = 'None';
$scope.items = [
    { name: 'John', otherProperty: 'Foo' },
    { name: 'Joe', otherProperty: 'Bar' }
};

$scope.menuOptions = [
    {
        name: 'Select',
        iconClass: 'glyphicon glyphicon-ok-circle',
        onClick: function ($itemScope) {
            $scope.selected = $itemScope.item.name;
        }
    },
    null, // Dividier
    {
        name: 'Remove',
        iconClass: null,  //no icon
        onClick: function ($itemScope) {
            $scope.items.splice($itemScope.$index, 1);
        }
    }
];
```

## Menu Options

Every menu option is an object with named properties. Most items will use the `{name: String, iconClass: String, onClick: Function}` format. If you need a dynamic item in your context menu you can also use the `[name: Function, iconClass: Function, onClick: Function]` format.

```js
$scope.menuOptions = [
    [function ($itemScope) { return $itemScope.item.name; }, function ($itemScope) {
        // Code
    }]
];
```

## Style Overlay

To give a light darker disabled tint while the menu is open add the style below.

```css
body > .dropdown {
    background-color: rgba(0, 0, 0, 0.1);
}
```

## Limitations (work in progress)

Nested lists are not supported yet, because I have not needed it yet. If you add it please do a pull request.

```JS
$scope.menuOptions = [
    ['Parent Item 1', function ($itemScope) {
        // Code
    },  ['Child Item 1', function ($itemScope) {
            // Code
        }],
        ['Child Item 2', function ($itemScope) {
            // Code
        }]
    ]
];
```
