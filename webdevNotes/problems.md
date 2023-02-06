favicon, hover, cursor

# Problem during Web Development

## How to prevent favicon requests
- Browser requests `favicon` when site has and asks for none.
 

### [Solution](https://stackoverflow.com/questions/1321878/how-to-prevent-favicon-ico-requests)
Add to `html` `head` tag:
```html
<link rel="icon" href="data:,">
```

## Problems with hover
- hover style only works for a second when element is clicked but not on hover
- chrome dev tool shows correct styles when checking forced hover status
- problem only happens with dev tools open, and set to repsonsive mode
- beside hovering problem cursor is not arrow but a circle

### [Solution](https://stackoverflow.com/questions/17842984/google-chrome-shows-gray-circle-cursor):
- Problem is that the device is set to
 mobil touch mode.
- Click on responsive mode menu (three dots) and select `Add Device Type` and select `Mobile (no touch)`, you can only see device type in top row if row is wide enough