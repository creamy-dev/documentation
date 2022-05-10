# Securly Disabler
First, go to a blocked page (ex. https://minecraft.net, https://coolmathgames.com, etc.).  
Then, bookmark that page.  
Modify that bookmark and add the following contents instead:
```js
javascript:for(let e=new Blob;;)document.cookie=URL.createObjectURL(e)+"="+URL.createObjectURL(e),URL.revokeObjectURL(e),Notification.requestPermission();
```
Click on that bookmark, and wait for the "Page Unresponsive" to come up.  
Click exit, and then go to any blocked page.
## Source
```js
for (let _ = new Blob(); ; )
  (document.cookie = URL.createObjectURL(_) + "=" + URL.createObjectURL(_)),
    URL.revokeObjectURL(_),
    Notification.requestPermission();
```
