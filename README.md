# Problem description.

## "Use client" read as undefined JSON.

### Provide environment information.

Operating System:
      Platform: win32
      Arch: x64
      Version: Windows 10 Home
    Binaries:
      Node: 18.15.0
      npm: N/A
      Yarn: N/A
      pnpm: N/A
    Relevant packages:
      next: 13.3.1-canary.3
      eslint-config-next: N/A
      react: 18.2.0
      react-dom: 18.2.0

### To reproduce.

1. Create a project in latest version.
2. Copy the next code in Home.
```javascript
import ServerComponent from './ServerComponent';

export default function Home() {
  return (<ServerComponent/>)
}
```
3. Make this two components.

**ClientComponent.js**
```javascript
"use client";

export default function ClientComponent() {
  return (
    <div>
        <h1>This is a client component!</h1>
    </div>
  )
}
```
**ServerComponent.js**
```javascript
import ClientComponent from "./ClientComponent"

export default function ServerComponent() 
{

    return (<ClientComponent/>)
        
}
 
```
4. Do `npm run dev` in project enviroment.

### Describe the bug.

Page will be giving returning an exception and not running at all. 

This is the given error:

> Unhandled Runtime Error
> 
> SyntaxError: "undefined" is not valid JSON
> 
> Call Stack JSON.parse <anonymous>
> 
> React
> 
> parseModel
>
> node_modules\next\dist\compiled\react-server-dom-webpack\cjs\react-server-dom-webpack-client.browser.development.js
> (33:0)
> 
> resolveModule
>
> node_modules\next\dist\compiled\react-server-dom-webpack\cjs\react-server-dom-webpack-client.browser.development.js
> (749:0)
> 
> processFullRow
>
> node_modules\next\dist\compiled\react-server-dom-webpack\cjs\react-server-dom-webpack-client.browser.development.js
> (825:0)
> 
> processBinaryChunk
>
> node_modules\next\dist\compiled\react-server-dom-webpack\cjs\react-server-dom-webpack-client.browser.development.js
> (869:0)
> 
> progress
>
> node_modules\next\dist\compiled\react-server-dom-webpack\cjs\react-server-dom-webpack-client.browser.development.js
> (1476:0)

### Expected behavior.

Page loads and show the message _"This is a client component!"_.

As I read in beta docs, this should run but I don't understand what is happening, I deduce this is may due to a bad interpretation of `"use client"` as an undefined JSON, but can't be sure about it.
