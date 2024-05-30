# VsCodeSnippets
## How to use snippets in VS Code

## Step 1: Download the latest VS Code
- Search for `vscode download` or go to https://code.visualstudio.com/download
- leave all the defaults selected when going through the installer

## Step 2: Open VS Code and sign in
- Once you opened VS Code sign in using the profile icon on the bottom left of the screen
- Make sure to sign in with either your `github` or `microsoft account` (university or personal)
- I recommend using a `github` account since you can test if the snippets are syncing
- Make sure `setting sync` and `cloud changes` is on

## Step 3: Open the user snippets config file
- Once you've signed in all your snippet config files will sync
- To edit your snippets click on the settings icon on the bottom left of the screen
- Then click on `user snippets`
- This will show you all your existing snippets config files or you can create a new one
- You can make snippets for any language (javascript, css, html, etc...)
- For example
  - Search for javascript and select the `javascript.json` (not javascriptreact)
  - This will hold all the snippets you want to use in a `.js` file

## Step 4: Edit the user snippet config file
- Now you will see a file called `langaugeName.json` for this example you will see `javascript.json`
- If this is the first time opening this file then you will see a default comment explaining how to use the config file
- You can ignore this since AI can do this for us
- Delete everything in the file if you want to start fresh

## Step 5: How the config file stores the snippets
- Before you let AI right the code understand that this file is an object of objects
- This means that the basic layout looks like this
``` 
{
  "snippet name 1" : {
      "prefix": "snip_1" //This is what you want to type to call the snippet into your .js file
      code for the snippet
  }, // This comma separates the snippets from each other
  "snippet name 2" : {
      "prefix": "snip_2"
      code for the snippet
  },// Again this comma separetes the snippets. AI doesnt take this into account
}
```

## Step 6: Prompt AI to make a user snippet 
- You can make a snippet of any text for example lets make a snippet for a multiplyMatrix function
- This is the code for that function that I want to make a snippet of
```
    function multiplyMatrices(matrixA, matrixB) {
        let result = new Array(16).fill(0);
        for (let i = 0; i < 4; i++) {
            for (let j = 0; j < 4; j++) {
                for (let k = 0; k < 4; k++) {
                    result[i * 4 + j] += matrixA[i * 4 + k] * matrixB[k * 4 + j];
                }
            }
        }
        return result;
    }
```
- Prompt AI with this message (BingAI or chatGPT or whatever)
```
Make a vsCode snippet for 
    function multiplyMatrices(matrixA, matrixB) {
        let result = new Array(16).fill(0);
        for (let i = 0; i < 4; i++) {
            for (let j = 0; j < 4; j++) {
                for (let k = 0; k < 4; k++) {
                    result[i * 4 + j] += matrixA[i * 4 + k] * matrixB[k * 4 + j];
                }
            }
        }
        return result;
    }
```
- The AI will give you code somthing like this
```
{
    "Matrix Multiplication": {
        "prefix": "multiplyMatrices",
        "body": [
            "function multiplyMatrices(matrixA, matrixB) {",
            "    let result = new Array(16).fill(0);",
            "    for (let i = 0; i < 4; i++) {",
            "        for (let j = 0; j < 4; j++) {",
            "            for (let k = 0; k < 4; k++) {",
            "                result[i * 4 + j] += matrixA[i * 4 + k] * matrixB[k * 4 + j];",
            "            }",
            "        }",
            "    }",
            "    return result;",
            "}"
        ],
        "description": "Function to multiply two 4x4 matrices"
    }
}
```
- Remember that this assumes that there are no other snippets already in the config file
- If this is the first and only snippet then copy and paste this exact code in the config file
- See `step 7` to try this out before adding another
- If you want to add another snippet to the existing config file
- Prompt the AI with the new code you want to use as a snippet
- For example I have a fragment shader source code that I gave to AI and it gives this code
```
{
    "Fragment Shader Source Code": {
        "prefix": "snip_fragmentShaderSourceCode", //I like to use snip_name to differentiate between normal code and calling a snippet within the code, doing this also list all your snippets when you type snip_ then you can select the one you want with the arrow keys
        "body": [
            "const fragmentShaderSourceCode =`",
            "    precision mediump float;",
            "",
            "    varying vec3 vColor;",
            "",
            "    void main() {",
            "        gl_FragColor = vec4(vColor, 1);",
            "    }",
            "`;"
        ],
        "description": "Snippet for Fragment Shader Source Code"
    }
}
```
- You can't just past this code in as is. Only copy what is needed to make the config file look like this
```
{ //This is start of the main object bracket
    "Matrix Multiplication": {
        "prefix": "snip_multiplyMatrices",
        "body": [
            "function multiplyMatrices(matrixA, matrixB) {",
            "    let result = new Array(16).fill(0);",
            "    for (let i = 0; i < 4; i++) {",
            "        for (let j = 0; j < 4; j++) {",
            "            for (let k = 0; k < 4; k++) {",
            "                result[i * 4 + j] += matrixA[i * 4 + k] * matrixB[k * 4 + j];",
            "            }",
            "        }",
            "    }",
            "    return result;",
            "}"
        ],
        "description": "Function to multiply two 4x4 matrices"
    }, // Don't forget this comma
    "Fragment Shader Source Code": {
        "prefix": "snip_fragmentShaderSourceCode",
        "body": [
            "const fragmentShaderSourceCode =`",
            "    precision mediump float;",
            "",
            "    varying vec3 vColor;",
            "",
            "    void main() {",
            "        gl_FragColor = vec4(vColor, 1);",
            "    }",
            "`;"
        ],
        "description": "Snippet for Fragment Shader Source Code"
    }, // Add a comma here for later
}//This is end of the main object bracket
```

## Step 7: Using the snippet
- There is a separate config file for each langauge as mentioned earlier so the snippets will only work for its specific language from its specifc config file
- For example all the snippets in the `javascript.json` file can only be used in any `.js` files
- Open a file in vscode that you made the snippet for
- For example in a `main.js` file
- Start typing whatever prefix name you have it set to and you will see suggestions pop up
- I mentioned in `step 6` to start naming the prefix like `snip_name` so that when you type `snip_` you will see all your snippets show up
- Select the one you want with the arrows and press enter
- It will paste in your snippet

## Steo 8: Check that your snippets are syncing with VS Code
- This works only with a github account
- go to github.com and sign in to the account that you used for VS code
- Then go to any repoistory even this exact one
- press the . (>) key next to the question mark and you will see VS code open in the browser
- You should be automatically signed in
- Then go to the user snippets config file and check that the file is the same as your VS code app

## Theres a snippets example file called javascript.json to test it out if something went wrong

