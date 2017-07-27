Speex Codec in Javascript
=========================

Speex Codec in Javascript. Ported speex-1.2.0RC using emscripten tool. 

* Both encoder and decoder (see [demo](http://jpemartins.github.com/speex.js/))

* [aurora.js](http://github.com/ofmlabs/aurora.js) integration (see [demo](http://jpemartins.github.com/speex.js/aurora.html))

(Microphone loopback is only working in Firefox.)

 播放网络 数据：ogg 转 wav
 
     var samples, sampleRate;
     var xhr = new XMLHttpRequest();
     xhr.open("get", "https://image-public.touhaozhubo.com/video2017072415145513096056530311.spx", true);
     // 下载 数据
     xhr.responseType = "blob";// 以二进制下载 数据
     xhr.onreadystatechange = function() {
     if (xhr.readyState == 4 && xhr.status == 200) {
       console.log(xhr.response);
       var blob =  xhr.response;
       var reader = new FileReader();// 用 FileReader 读取 blob 数据
       reader.addEventListener("loadend", function() {
       var data = reader.result;
       // var data =  xhr.response,
       var  ret, header;
       ret = Speex.decodeFile(data);
       samples = ret[0];
       header = ret[1];
       sampleRate = header.rate;
       addDownloadLink("test"+".wav", "#file_ogg",samples, "audio/wav");
       Speex.util.play(samples, sampleRate);
      });
     reader.readAsBinaryString(blob); // 将文件读取为二进制编码
     }
     };
     xhr.send(null);
