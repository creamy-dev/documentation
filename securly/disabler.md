# Securly Disabler
This can disable securly by overloading packet sizes.
## Install
First, go to a blocked page (ex. https://minecraft.net, https://coolmathgames.com, etc.).  
Then, bookmark that page.  
Modify that bookmark and add the following contents instead:
```js
javascript:if("https://useast-www.securly.com"!==window.location.origin)throw"flying bird";window.cookie="";var _=new Blob;function sleep(e){return new Promise(o=>setTimeout(o,e))}async function main(){for(let e=0;e<1500;e++)document.cookie=URL.createObjectURL(_)+"="+URL.createObjectURL(_),URL.revokeObjectURL(_),document.title="🐦 "+e+"/1500",await sleep(10);document.title="🐦 Done!",window.location.replace("https://google.com")}main();
```
Click on it, and wait for it to redirect you to google.
## Uninstall
Go to https://useast-www.securly.com/404.html, and click on the padlock.  
After that, click on cookies.  
Click on securly.com, and click remove.  
And click on useast-www.securly.com, and click remove.  
Click done.
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
