
<html>
<!-- 
  Copyright Indra Soluciones Tecnologías de la Información, S.L.U.
  2013-2019 SPAIN
 
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at
       http://www.apache.org/licenses/LICENSE-2.0
  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License. 
-->

<head>
    <title>Market Gadgets</title>
    <!-- Latest compiled and minified CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">

    <!-- jQuery library -->
    <script src="https://code.jquery.com/jquery-3.5.1.js"></script>
  
    <!-- Popper JS -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>

    <!-- Latest compiled JavaScript -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
    
    
    <style>
        .btn {
            width: 160px;
        }
        
    </style>

<script src="https://unpkg.com/@isomorphic-git/lightning-fs"></script> 
<script src="https://unpkg.com/isomorphic-git"></script> 
<script type="module"> 
import http from 'https://unpkg.com/isomorphic-git@beta/http/web/index.js' 
     window.fs = new LightningFS('fs',{'wipe':true}) 
     window.dir = '/market' 
     window.url = '/market/gadgets'
    git.clone({ fs, http, dir, url: 'https://github.com/dsanteodoro/testpages', corsProxy: 'https://cors.isomorphic-git.org',force: true }).then(function (data){
        fs.promises.readdir(window.url).then(function(data){
            console.log(data)
            for(var i = 0; i< data.length;i++){
                var url = window.url+'/'+data[i];               
                loadfiles(url);
            }
            })}) 

function loadfiles(url){
    fs.promises.readdir(url).then(function(dataGadget){
                //read json and image files for gadget.
                var hash = Math.random().toString(36).substring(7);
               $('#gadgetslist').append('<tr id="'+hash+'"><td></td><td></td></tr>')
                console.log(dataGadget);
                
                fs.promises.readFile(url+'/info.json',{encoding:'utf8'}).then(function(data){
                   var dat =  JSON.parse(data);
                   console.log(url);
                    console.log(dat);
                    $('#gadgetslist td').eq( 1 ).replaceWith('<td><label>'+dat.identification+'</label></td>');
                });
                fs.promises.readFile(url+'/image.png').then(function(data){ 
                    console.log(url);                   
                    console.log(data);
                    
                    $('#gadgetslist td').eq( 0 ).replaceWith('<td><img src="data:image/png;base64,'+  btoa(String.fromCharCode.apply(null, new Uint8Array(data))) +'" ></td>');
                });
                })
}

function utf8_to_b64( str ) {
  return window.btoa(unescape(encodeURIComponent( str )));
}


</script> 
 


</head>

<body>   
<table id="gadgetslist">
    <tr>
    <th>image</th>
    <th>text</th>
    </tr>
</table>

 
</body>



</html>
