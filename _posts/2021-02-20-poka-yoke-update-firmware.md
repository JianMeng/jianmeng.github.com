---
title: "poka yoke update firmware"
permalink: blog/poka-yoke-update-firmware.html
layout: post
fuzzydate: February 2021
---

["poka yoke"](https://kanbanize.com/lean-management/improvement/what-is-poka-yoke) is a japanese word ポカヨケ, which mean Fool-proofing. I first meet this word in a book talking about User interface design in web serval years ago. But soon I found where it should be applied.

My boss in Emerson assignd me to write a update firmware page in site supervisor. This is a simple page like below.

<figure class="image">
  <img src="../assets/update_firmware.png" alt="update firmware wireframe" title="update firmware wireframe"/>
</figure>

The user first choose a firmware file by click choose fireware button. It tigger a file chooser popup by OS. Then it start to upload file to backend server. After server received the whole file, CRC and file version should be checked first. Then the normal update progress finally start, including boot loader, the os image write to some memory etc.

<div class="mermaid">
sequenceDiagram
    participant b as Browser
    participant s as Server
    b->>s: upload firmware
    s-->>b: received
    alt happy path
      Note over b,s: websocket message
      s-->>b: file name, reversion, file size
      Note right of s: upload event did happen.
      s-->>b: erase memory
      s-->>b: update ....
    end
    alt unhappy path
      Note over b,s: websocket message
      s-->>b: err
    end
</div>

The firmware is about 64MB big. Its name is like ver-XXXX.Pkg. But that can be rename file evilly by human Uploading that to server takes a while. Then your user can know whether the file is right by server notification. Server know it because it has a 100 line C function from the header part of the firmware. Waiting for message from backend server is time consuming. 

Our customer is mainly cell store on the highway and large supermarket. But realy the end user is the heating and ventilation engineer from our company, whose job is configure all kind HAVC, refrigerator and light etc devices. They are busy, really know all kind sensor data's meaning, and what to do with that infomation. Sometime they need update firmware to solve particularly problem. But they are human. Human have the right to make mistake. 

In above operation, file name can be rename. So user can not know the right reversion immediatly. Backend message will tell that after uploading process eventually. But that message flush by new message from backend. The user can negelect that. When the wrong firmware is installed in hardware, the shop may suffer from food went bad to air condition disfunction. Huge cost may got someone fired. I feel i could do something to improve that, at least for the part of selecting right reversion of firmare. Afterall, if you make your customer feel theirself stupid after using your device, you are the one should be blamed.

At that time, web browser provide some juicy new function called [File Reader](https://developer.mozilla.org/en-US/docs/Web/API/FileReader) and [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer). It can do c function part in browser side once after user select file from OS side. User can know firmware version immedately. That is cool.

There is a [browser crash](https://joji.me/en-us/blog/processing-huge-files-using-filereader-readasarraybuffer-in-web-browser/) if file choosed is larger than About 600MB. But since the firmware could large than 2 size of memory. So we can early out those case maybe cause by user mistake.

<div class="mermaid">
sequenceDiagram
    participant m as main thread
    participant w as worker
    Note over m,w: myWorker = new Worker("my_task.js");
    m->>m: file = document.getElementById('file').files[0];
    alt user choose a large wrong file
      m->>m: error if file.size > 2 * memory size 
      m->>m: update error message.
    end
    alt happy path
      m->>m: read slice of file by filereader readAsArrayBuffer
      m->>w: send result from filereader onload event
      w->>w: calculate crc, filename, reversion by Uint8Array
      w-->>m: send above back
      m->>m: display the result before upload
    end
</div>

One may ask what about the user which do not have such browser. The answser is simple. They will do the old way. Server will tell whether firmware is good. Different browser have different behaivor based on ability.

A little bad thing i found in above approach was when read the large file is taking some time for browser calculation. So there ware a short freeze in browser. The undesirable effect soon be eliminated by introduce [web worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers). Now the browser will have async read and analysis file. The main thread just send file content and wait for json result from web worker. 

Two episodes: 

One.

In one morning i got complain email from QA. The user said the file size is wrong. After a few digging, that cause by linux and window are different about 1kB?= 1000B or 1024B. After i put the whole number byte aside, world peace.

Two.

Our company work in agile process. The UI designer actually are in charge UI. It is not that man's design.  But he will be blamed if it not rock. Put it in simple way, it is not a right process result. My doing stealthily release in a inside version. My boss was very keen to notice the change of page, since he did a lot firmware update to check product status everyday. He shooted an email inquiring how it work personally. I replyed. Weeks flyed sliently. But my teamleader disagree to put that in product because of its bastard status. Then he required me to rollback the change. I follow the order later. Then my boss and internal user ask it add it back. I guess they finally express their love.

Now that bastard become legitimate citizen in  "4.12.1 Firmware Update - Remote Access" of [site supervisor user guide](https://climate.emerson.com/documents/site-supervisor-user-guide-rev-17-en-us-6471528.pdf).

The agile process sometime hinders people design. One day later my designer encouraged me to be a designer. It  astonish me.  I admit I have good sense of appreciating beauty. But make myself a Vinci is another thing. I am bad at colors. Above work started by good willness to help people reduce they day work. Innovate is not like your payroll received every month punctuality. I did a lot observation and learning. Then I know what I can improve. But making innovate as my everyday output only got me more chance to be fired. :D


