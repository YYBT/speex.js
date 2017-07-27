Speex Codec in Javascript
=========================

Speex Codec in Javascript. Ported speex-1.2.0RC using emscripten tool. 

* Both encoder and decoder (see [demo](http://jpemartins.github.com/speex.js/))

* [aurora.js](http://github.com/ofmlabs/aurora.js) integration (see [demo](http://jpemartins.github.com/speex.js/aurora.html))

(Microphone loopback is only working in Firefox.)

播放网络 数据：


<code>var samples, sampleRate;

  var xhr = new XMLHttpRequest();
  // xhr.overrideMimeType("audio/ogg;charset=US-ASCII");
  xhr.open("get", "https://image-public.touhaozhubo.com/video2017072415145513096056530311.spx", true);
  xhr.responseType = "blob";
  xhr.onreadystatechange = function() {
    if (xhr.readyState == 4 && xhr.status == 200) {
      console.log(xhr.response);

var blob =  xhr.response;
      var reader = new FileReader();
      reader.addEventListener("loadend", function() {
        var data = reader.result;

        // var data =  xhr.response,
        var  ret, header;
        ret = Speex.decodeFile(data);
        samples = ret[0];
        header = ret[1];
        sampleRate = header.rate;
        addDownloadLink("test"+".wav", "#file_ogg",
          samples, "audio/wav");

        Speex.util.play(samples, sampleRate);

         // reader.result contains the contents of blob as a typed array
      });
      reader.readAsBinaryString(blob);




    }
  };
  xhr.send(null);</code>
