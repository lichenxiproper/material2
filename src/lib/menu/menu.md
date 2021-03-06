`<md-menu>` is a floating panel containing list of options.

<!-- example(menu-overview) -->

By itself, the `<md-menu>` element does not render anything. The menu is attached to and opened
via application of the `mdMenuTriggerFor` directive:
```html
<md-menu #appMenu="mdMenu">
  <button md-menu-item> Settings </button>
  <button md-menu-item> Help </button>
</md-menu>

<button md-icon-button [mdMenuTriggerFor]="appMenu">
   <md-icon>more_vert</md-icon>
</button>
```

### Toggling the menu programmatically
The menu exposes an API to open/close programmatically. Please note that in this case, an
`mdMenuTriggerFor` directive is still necessary to attach the menu to a trigger element in the DOM.

```ts
class MyComponent {
  @ViewChild(MdMenuTrigger) trigger: MdMenuTrigger;

  someMethod() {
    this.trigger.openMenu();
  }
}
```

### Icons
Menus support displaying `md-icon` elements before the menu item text.

*my-comp.html*
```html
<md-menu #menu="mdMenu">
  <button md-menu-item>
    <md-icon> dialpad </md-icon>
    <span> Redial </span>
  </button>
  <button md-menu-item disabled>
    <md-icon> voicemail </md-icon>
    <span> Check voicemail </span>
  </button>
  <button md-menu-item>
    <md-icon> notifications_off </md-icon>
    <span> Disable alerts </span>
  </button>
</md-menu>
```

### Customizing menu position

By default, the menu will display below (y-axis), after (x-axis), and overlapping its trigger.
The position can be changed using the `xPosition` (`before | after`) and `yPosition`
(`above | below`) attributes. The menu can be be forced to not overlap the trigger using
`[overlapTrigger]="false"` attribute.

```html
<md-menu #appMenu="mdMenu" yPosition="above">
  <button md-menu-item> Settings </button>
  <button md-menu-item> Help </button>
</md-menu>

<button md-icon-button [mdMenuTriggerFor]="appMenu">
  <md-icon>more_vert</md-icon>
</button>
```

### Nested menu

Material supports the ability for an `md-menu-item` to open a sub-menu. To do so, you have to define
your root menu and sub-menus, in addition to setting the `[mdMenuTriggerFor]` on the `md-menu-item`
that should trigger the sub-menu:

```html
<md-menu #rootMenu="mdMenu">
  <button md-menu-item [mdMenuTriggerFor]="subMenu">Power</button>
  <button md-menu-item>System settings</button>
</md-menu>

<md-menu #subMenu="mdMenu">
  <button md-menu-item>Shut down</button>
  <button md-menu-item>Restart</button>
  <button md-menu-item>Hibernate</button>
</md-menu>

<button md-icon-button [mdMenuTriggerFor]="rootMenu">
  <md-icon>more_vert</md-icon>
</button>
```


### Keyboard interaction
- <kbd>DOWN_ARROW</kbd>: Focuses the next menu item
- <kbd>UP_ARROW</kbd>: Focuses previous menu item
- <kbd>RIGHT_ARROW</kbd>: Opens the menu item's sub-menu
- <kbd>LEFT_ARROW</kbd>: Closes the current menu, if it is a sub-menu.
- <kbd>ENTER</kbd>: Activates the focused menu item
