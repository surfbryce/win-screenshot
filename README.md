# Windows Screenshot Library for JS Lovers

> :rocket: :telescope: A mighty, robust screenshot library for Windows, Electron and Node.JS Developers.

<strong>Screenshot type offered by this library:</strong>
1) Coordinate Based or Specific Region (x1, y1, x2, y2)
2) Full Screen
3) Windows Working Area only (taskbar is excluded)
3) Only Taskbar
4) All Active Windows at once

<strong>What so special about this library: </strong>
1) It is capable of finding accurate coordinates of an Active Window or Taskbar irrespective of the taskbar location (BOTTOM, LEFT, TOP, RIGHT) on the screen.
2) This is a Node.JS library but some part of the backend is developed using C#, which is useful for invoking Windows native methods easily.
3) All Active Windows can be screenshotted at once automatically just by calling a single method.
4) This library supports various image formats to save your screenshot in. (BMP, GIF, JPEG, PNG, TIFF).

```javascript
// ES6 Destructuring Assignment
const { Screenshot, ImageFormat } = require('win-screenshot');
const { writeFileSync } = require('fs');
const { homedir } = require('os');
const { spawnSync } = require('child_process');

// Destination Directory
const directoryName = `${homedir()}\\Desktop`;

let returnValues = Screenshot.captureAllWindows({
    // Use of PNG format for taking screenshot
    imageFormat: ImageFormat.PNG
});

// This is necessary as the return Value of captureAllWindows() is an array
for (let r of returnValues)  {
    // Now r contains an element from the array
    // You need to convert encoded base64 string into buffer before writing
    // This will save each screenshot with its process name.
    writeFileSync(`${directoryName}\\${r.processName}.png`, Buffer.from(r.imageBuffer, 'base64'));
}

// This will open the destination directory using cmd as inter-process communication call
spawnSync("cmd.exe", ["/c", `start ${directoryName}`]);
```

<h3>:clipboard: License: </h3> 
Licensed under the <a href="https://github.com/soulehshaikh99/win-screenshot/blob/master/LICENSE">MIT License</a>.
