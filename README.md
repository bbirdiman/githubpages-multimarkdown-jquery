# githubpages-multimarkdown-jquery

## github pages converted with multimarkdown using javascript

github pages is a great place to store light-markup text-files,
because you get version-control, and (mainly) it's cost-free.

i've looked around quite a bit, and as far as i can tell,
multimarkdown is the best markdown flavor  around.

its biggest problem is that multimarkdown doesn't have
a converter-routine written in javascript.

fortunately, the ever-clever brett terpstra created "marky",
a webservice geared to back-converting existing .html into markdown.

even better, though, marky can also convert markdown into .html,
and it uses multimarkdown to do that conversion.

and, because brett is really smart, marky has an a.p.i.

so you can use javascript to send your .mmd text to marky,
and have it returned as multimarkdown-converted .html.

so all you kids making markdown editors these days should be
using marky (and multimarkdown) to do your conversions.

appended is a sample .html file, with the code boiled down
to a simple minimum. let's not bother with a "license",
and just call it good old plain old public domain,
dedicated to making the world a better place.

obviously, i have taken this idea much further, so if you
would like me to post more, send me some of that star love.

''''
<!doctype html>
<head>
<meta http-equiv="Content-type" content="text/html;charset=UTF-8">
<title>
githubpages multimarkdown
</title>
<script src=http://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.0/jquery.min.js></script>
</head>
<body style=margin:0;padding:0>
<button onclick=dogetgithub() id=getgithub style=width:20%;height:60px>get github</button>
<button onclick=domarky() id=marky style=width:20%;height:60px>do marky</button><br>
<textarea id=thetext style=position:absolute;left:20px;top:66px;width:47%;bottom:0>http://fletcher.github.io/peg-multimarkdown/index.txt</textarea>
<div id=thehtml style=position:absolute;margin:0;padding:0;padding-right:20px;left:54%;top:0;right:0;bottom:0;overflow-x:hidden;overflow-y:auto></div>
<script type=text/javascript>
function dogetgithub(){
var theurl=$("#thetext").val()
if (theurl.substring(0,4) != "http"){theurl="http://fletcher.github.io/peg-multimarkdown/index.txt"}
$.ajaxSetup({cache:false})
$.ajax({
url: theurl,
dataType: 'text',
fail: function(data){$("#thetext").val(" fail! ");document.title=" fail! "},
success: function(data){$("#thetext").val(data)}
})
}</script>
<script type=text/javascript>
function domarky(){
$("#thehtml").html("calling marky...")
var result=""
var convertthis=$("#thetext").val()
$.post("http://heckyesmarkdown.com/go/",{domarkdown:1,text:convertthis,},function(result){
$("#thehtml").html(result)
})
}</script>
</body>
</html>
''''

that is all.
