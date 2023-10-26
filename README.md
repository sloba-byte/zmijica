
# Use typescript instead of javascript

### Just to debug in terminal & stuff
- Setup TSCompile:
(LINUX) First get https://github.com/nvm-sh/nvm so you can install proper version of NPM
(SHIT-WINDOWS) maybe this shit works but who knows & cares?
https://github.com/coreybutler/nvm-windows

- After installing NVM, open new terminal & run:
```bash
nvm install node
``` 
- Video contains step by step:
```
https://www.youtube.com/watch?v=JdvkaW2xeiI
```

- Navigate to folder were you want you app to be and then execute the following in terminal:

creates a package json
```bash
npm init -y
```

add dependecy in package.json for typescript
```bash
npm i typescript
```

setups tsconfig file. SourceMap part is important for debuging!
```bash
npx tsc --init --sourceMap --rootDir src --outDir lib
```

- Build task:

Next open VSCode and setup a tasks to watch index.ts file using TSC (create before that src/index.ts)

Hit ctrl+shift+p and search for "default build task" and hit enter.
After that search for tsc watch and again hit enter. This will create .vscode/tasks.json file.

After that hit ctrl+shift+b to start running the task.

Bonus: add this to task so it is executed each time you open folder in vscode:
```json
,"runOptions": {
    "runOn": "folderOpen"
}
```
- Launch/debug config for Node

Go to run and debug and click create a launch.json file (will be under .vscode folder again) and choose Node

Here change program to point to our index.js file in lib (the compiled typescript file):

```json
 "program": "${workspaceFolder}/lib/index.js",
```

And thats all folks
- BONUS2 (Multiple TS files - THIS IS NOT THAT USEFUL, BY THE WAY! USE COMMON.TS AND EXPORT!)
https://www.educba.com/typescript-export-function/

in tsconfig.json
```json
    "moduleDetection": "force",
```
This enables default seperation between different .ts files.
Example, in file1.ts you have type Song{..} and in file2.ts you can again have type Song{...}



### Basic way index.ts => index.js and include in index.html file
And this will include all the functions and stuff from .ts file. While we still can look at .ts and debug it regularly

```html
 <script src="lib/index.js"></script>
```
# Snake game requirements & how to:

1) Show "Snake" body & head in browser as a webpage (how to draw a snake exactly?)
    - How are we going to achive this? What does it mean in browser: 
    - HTML => mark with black color 1 pixel(DIV). By looking at it as a big grid (matrix) 
    - Snake board = (HTML)1 div, (CSS)Fixed pixel size (400x400px) with black border
    - Snake parts = 
    (HTML)
        NxN divs, dynamic from javascript (or typescript lets see later)
    (CSS) 
    ```css
    .snakePart {
        width: 10%;
        height: 10%;
        outline: 1px solid;
        float: left;
    }
    ```
    (JAVASCRIPT) = 
     get snakeBoard by id, and with 2 for loops add multiple divs with proper ID &  className = snakePart 
    ```js
  
    var iDiv = document.createElement('div');
    iDiv.id = i + '_' + j; 
    iDiv.className
    document.getElementById('snakeGame').appendChild(iDiv)
    ```

2) Move "Snake" with certian speed (use sleep, but find some optimal interval)
    ```css
    .on {
        background-color: black;
    }
    ```
    ```js
    document.getElementById('3_4').classList.add('on')

    //and to turn off pixel just
    document.getElementById('3_4').classList.remove('on')
    ```

    ```js
    //"make" movement each 200ms (5 times a second)
    intervalId = setInterval(moveOneStepRight, 200)
    //moveOneStepRight is function
    
    //when game over 
    clearInterval(intervalId)
    ```

    - Make sure to wrap things in classes and not have 10000 variables all over the place :)

    - Moving of snake is just adding offset +1, -1 or 0 To I & J positions.

    - Snake is just a list, and move is just: 1) Add new head 2) Remove old tail

    - In onload keyboard events:
    ```js
    document.onkeydown = (e) => {
        console.log("keydown:", e.code, " key:", e.key)

        switch(e.key) {
            case "ArrowUp":
            case "w":
                turnUp()
            break;

            case "ArrowDown":
            case "s":
                turnDown()
            break;

            case "ArrowLeft":
            case "a":
                turnLeft()
            break;

            case "ArrowRight":
            case "d":
                turnRight()
            break;
        }
   
      };
    ```

3) Take input from user (arrows or wasd), and change direction based on that (how to take input from user?)
    - Maybe it;s easier to just make buttons for starts, thats easy and we know it
    - Later figure out how to take input from keyboard

4) Food - when snake head eats food it should grow!


5) Wrap? What happens when snake hits a wall, dies or snake emerges to oposite side? - SNAKE DIES
When snake eats it self => DIES!


6) Score? Each time we eat food incrise some score by amount? Maybe latter add special time based food.


7) How do we start a game? When page loads game start, keep it simple stupid (KISS)

