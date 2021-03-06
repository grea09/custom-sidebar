# Custom Sidebar

This is an extra module for [Home Assistant Frontend](https://www.home-assistant.io/integrations/frontend/#extra_module_url) on [Home Assistant](https://www.home-assistant.io/)

This plugin allows you to rearrange items in the Home Assistant sidebar. (Overview, Map, History, etc)

Before                     |           After
:-------------------------:|:-------------------------:
![](https://raw.githubusercontent.com/Villhellm/README_images/master/sidebar-before-example.png)  |  ![](https://raw.githubusercontent.com/Villhellm/README_images/master/sidebar-example.png)

## HACS Installation and Configuration

### Step 1

Install Custom Sidebar plugin with HACS

### Step 2

By default this will only function if you load into a Lovelace view. To make sure this plugin works all the time make sure to follow the instructions all the way through.

To load the module into your instance you will need to add it to the frontend configuration in configuration.yaml.

Ex:
```yaml
frontend:
  extra_module_url:
    - /hacsfiles/custom-sidebar/custom-sidebar.js
```

### Step 3

The order configuration must be stored in `<config directory>/www/sidebar-order.yaml`. You will create this file yourself. All items will be under the root `order:`.
They will be arranged in order from top to bottom.

Ex:
```yaml
order:
  - item: map
    hide: true
  - item: developer tools
    href: /developer-tools/state
  - item: overview
  - item: history
    bottom: true
  - item: logbook
    bottom: true
```

## Manual Installation and Configuration

### Step 1

Install `custom-sidebar` by copying `custom-sidebar.js` from this repo to `<config directory>/www/custom-sidebar.js` on your Home Assistant instance.

### Step 2

To load the module into your instance you will need to add it to the frontend configuration in configuration.yaml.

Ex:
```yaml
frontend:
  extra_module_url:
    - /local/custom-sidebar.js
```

### Step 3

The order configuration must be stored in `<config directory>/www/sidebar-order.yaml`. You will create this file yourself. All items will be under the root `order:`.
They will be arranged in order from top to bottom.

Ex:
```yaml
order:
  - item: map
    hide: true
  - item: developer tools
    href: /developer-tools/state
  - item: overview
  - item: history
    bottom: true
  - item: logbook
    bottom: true
```

## Order

| Name | Type | Requirement | Description
| ---- | ---- | ------- | -----------
| order | list([item](#item-options)) | **Required** | List of items you would like to rearrange.

## Item Options

| Name | Type | Requirement | Description
| ---- | ---- | ------- | -----------
| item | string | **Required** | This is a string that will be checked for in the display name of the sidebar item. It can be a substring such as `developer` instead of `Developer Tools`. It is not case sensitive.
| bottom | boolean | **Optional** | Setting this option to `true` will group the item with the bottom items (Configuration, Developer Tools, etc) instead of at the top.
| hide | boolean | **Optional** | Hide item in sidebar.
| href | string | **Optional** | Define the href for the sidebar link.

## Exceptions
Exceptions can be used if you would like to define an order for a specific user/device.

| Name | Type | Requirement | Description
| ---- | ---- | ------- | -----------
| base_order | bool | **Optional** | If true this will run rearrangement for your base order configuration before running this exception. Default is false.
| user | string | **Optional** | Home Assistant user name you would like to display this order for.
| device | string | **Optional** | Type of device you would like to display this order for. ex: ipad, iphone, macintosh, windows, android
| not_user | string | **Optional** | Every Home Assistant user name *except* this user name.
| not_device | string | **Optional** | Every device *except* this device. ex: ipad, iphone, macintosh, windows, android
| order | [order](#order) | **Required** | Define and order. 

Ex sidebar-order.yaml using exceptions:
```yaml
order:
  - item: map
    hide: true
  - item: developer tools
    href: /developer-tools/state
  - item: overview
  - item: history
    bottom: true
  - item: logbook
    bottom: true
exceptions:
  - user: will
    base_order: true
    order:
      - item: map
        hide: false
      - item: developer_tools
        hide: true

```

NOTE: Notifications are not part of the same div as the other sidebar items; it is not moveable.

NOTE: If you are using a language other than English make sure to include both the English word and a second entry with the translated word that is displayed in your browser for the `item: ` portion of the config. This will ensure that the item is moved/hidden regardless of the time at which it is rendered.
Example: Language Portuguese
```yaml
  - item: history
    hide: true
  - item: Histórico
    hide: true
```
