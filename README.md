Sites in One
---

### TODO
##### Link it
* Config
  * locate context
```yaml
cursorElement:
	element
	classNames: []
currentElement: # auto update during locating
	element
	classNames: []
```
  * transform context
```yaml
origin: ""
current: ""
```
  * config
```yaml
locate:
  - type: selector, # "selector"
    args:
      - ":contains('name')" # jQuery selector
    search: child # "child", "before", "after", "domain"
    setContext:
      pickElement: this
watch:
  - {} # TODO resonate with `locate`
action:
  - type: "link"
    transforms:
      - type: "regex"
        args: [],
        setContext:
          matches: "matches"
        format: "http://example.com/User-${matches[0]}" // lodash index rule
```
##### Fetch data on page
* context
```yaml
url: "http://example.com/wh/*" # pattern
fetch:
  type: "HTTP"
  args:
    - "GET",
    - "http://example.com/api/..." # url
    - "params" # params
    - "body" # body
  transform:
    - type: "get",
      args:
        - "data[0]"
render:
  data: "current" # "" = "current", lodash `get`
  type: "div"
  text: ""
  style: ""
  children:
    - data: "current",
      type: "ul"
      text: "",
      style: "",
      children:
        - data: "current[${i}]",
          type: "li"
          text: "",
          style: "",
          click: "setupData",
          children:
            - type: "div"
```
##### Setup data
```yaml
events:
  - name: "setupData",
    action:
      - locate: []
        transform: []
```
