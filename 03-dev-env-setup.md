# 🖥️ Web Development Environment Setup

This guide will help you set up a **development environment for HTML, CSS, and JavaScript**.

---

## 1. Install a Code Editor

We recommend **Visual Studio Code (VS Code)**:

- Download: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- Install it and open the editor.

### Recommended VS Code Extensions

- **Live Server** – run HTML files with live reload.
- **Prettier** – auto-format code.
- **HTML CSS Support** – improved CSS autocomplete.

---

## 2. Install a Web Browser

You need a browser to see your projects:

- **Google Chrome**: [https://www.google.com/chrome/](https://www.google.com/chrome/)  
- **Firefox**: [https://www.mozilla.org/firefox/](https://www.mozilla.org/firefox/)

> Tip: Use DevTools (Right-click → Inspect) to debug HTML, CSS, and JS.

---

## 3. Create Your Project Folder

Create a folder structure like this:

```
web-project/
├─ index.html
├─ style.css
└─ script.js
```


- Create a folder named `web-project`.
- Add three files: `index.html`, `style.css`, and `script.js`.

---

## 4. HTML Starter Template

Open `index.html` and add:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Web Project</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Hello, world!</h1>
  <button id="myButton">Click Me</button>

  <script src="script.js"></script>
</body>
</html>
```

## 5. Add CSS Styles

Open style.css and add:

```css
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  text-align: center;
  margin: 0;
  padding: 50px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
```


## 6. Add JavaScript

Open `script.js` and add the following code:

```javascript
const button = document.getElementById('myButton');

button.addEventListener('click', () => {
  alert('Button clicked!');
});
```


## 7. Run Your Project

### Option 1: Open in Browser
- Double-click `index.html` to open it in your browser.

### Option 2: Using Live Server (Recommended)
1. Open VS Code.
2. Open your project folder.
3. Right-click `index.html` → **Open with Live Server**.
4. Your project will open in a browser and automatically refresh when you save changes.
