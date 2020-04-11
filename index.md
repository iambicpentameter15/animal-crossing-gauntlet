<font face="helvetica">

<div><div id="603446273904584399" align="left" style="width: 100%; overflow-y: hidden;" class="wcustomhtml"><script type="text/javascript">
<!--
//*********************************************************
//
// Please feel free to add to this list.
//
// You can change names in the list.
// I wrote names in quotation marks, and separated them with commmas.
// Please don't put a comma at the end though.
//
//*********************************************************

var namMember = new Array(
    "Admiral (Cranky Bird)",
    "Agent S (Peppy Squirrel)",
    "Agnes (Sisterly Pig)",
    "Al (Lazy Gorilla)",
    "Alfonso (Lazy Alligator)",
    "Alice (Normal Koala)",
    "Alli (Snooty Alligator)",
    "Amelia (Snooty Eagle)",
    "Annabelle (Peppy Anteater)",
    "Anchovy (Lazy Bird)", 
    "Ankha (Snooty Cat)",
    "Angus (Cranky Bull)",
    "Anicotti (Peppy Mouse)",
    "Annalisa (Normal Anteater)",
    "Annalise (Snooty Horse)",
    "Antonio (Jock Anteater),
    "Apollo (Cranky Eagle)",
    "Apple (Peppy Hamster)",
    "Astrid (Snooty Kangaroo)",
    "Audie (Peppy Wolf)",
    "Zucker (Lazy Octopus)"
    );
//*********************************************************

var lstMember = new Array();
var parent = new Array();
var equal = new Array();
var rec = new Array();
var cmp1,cmp2;
var head1,head2;
var nrec;

var numQuestion;
var totalSize;
var finishSize;
var finishFlag;

//The initialization of the variable+++++++++++++++++++++++++++++++++++++++++++++
function initList(){
    var n = 0;
	var mid;
	var i;

	//The sequence that you should sort
	lstMember[n] = new Array();
	for (i=0; i<namMember.length; i++) {
		lstMember[n][i] = i;
	}
	parent[n] = -1;
	totalSize = 0;
	n++;

	for (i=0; i<lstMember.length; i++) {
		//And element divides it in two/more than two
		//Increase divided sequence of last in first member
		if(lstMember[i].length>=2) {
			mid = Math.ceil(lstMember[i].length/2);
			lstMember[n] = new Array();
			lstMember[n] = lstMember[i].slice(0,mid);
			totalSize += lstMember[n].length;
			parent[n] = i;
			n++;
			lstMember[n] = new Array();
			lstMember[n] = lstMember[i].slice(mid,lstMember[i].length);
			totalSize += lstMember[n].length;
			parent[n] = i;
			n++;
		}
	}

	//Preserve this sequence
	for (i=0; i<namMember.length; i++) {
		rec[i] = 0;
	}
	nrec = 0;

	//List that keeps your results
	//Value of link initial
	// Value of link initial
	for (i=0; i<=namMember.length; i++) {
		equal[i] = -1;
	}

	cmp1 = lstMember.length-2;
	cmp2 = lstMember.length-1;
	head1 = 0;
	head2 = 0;
	numQuestion = 1;
	finishSize = 0;
	finishFlag = 0;
}

//&#12522;&#12473;&#12488;&#12398;&#12477;&#12540;&#12488;+++++++++++++++++++++++++++++++++++++++++++
//flag&#65306;Don't know characters
//  -1&#65306;Chose the left
//   0&#65306;Tie
//   1&#65306;Chose the right
function sortList(flag){
	var i;
	var str;

	//rec preservation
	if (flag<0) {
		rec[nrec] = lstMember[cmp1][head1];
		head1++;
		nrec++;
		finishSize++;
		while (equal[rec[nrec-1]]!=-1) {
			rec[nrec] = lstMember[cmp1][head1];
			head1++;
			nrec++;
			finishSize++;
		}
	}
	else if (flag>0) {
		rec[nrec] = lstMember[cmp2][head2];
		head2++;
		nrec++;
		finishSize++;
		while (equal[rec[nrec-1]]!=-1) {
			rec[nrec] = lstMember[cmp2][head2];
			head2++;
			nrec++;
			finishSize++;
		}
	}
	else {
		rec[nrec] = lstMember[cmp1][head1];
		head1++;
		nrec++;
		finishSize++;
		while (equal[rec[nrec-1]]!=-1) {
			rec[nrec] = lstMember[cmp1][head1];
			head1++;
			nrec++;
			finishSize++;
		}
		equal[rec[nrec-1]] = lstMember[cmp2][head2];
		rec[nrec] = lstMember[cmp2][head2];
		head2++;
		nrec++;
		finishSize++;
		while (equal[rec[nrec-1]]!=-1) {
			rec[nrec] = lstMember[cmp2][head2];
			head2++;
			nrec++;
			finishSize++;
		}
	}

	//Processing after finishing with one list
	if (head1<lstMember[cmp1].length && head2==lstMember[cmp2].length) {
		//List the remainder of cmp2 copies, list cmp1 copies when finished scanning
		while (head1<lstMember[cmp1].length){
			rec[nrec] = lstMember[cmp1][head1];
			head1++;
			nrec++;
			finishSize++;
		}
	}
	else if (head1==lstMember[cmp1].length && head2<lstMember[cmp2].length) {
		//List the remainder of cmp1 copies, list cmp2 copies when finished scanning
		while (head2<lstMember[cmp2].length){
			rec[nrec] = lstMember[cmp2][head2];
			head2++;
			nrec++;
			finishSize++;
		}
	}

	//When it arrives at the end of both lists
	//Update a pro list
	if (head1==lstMember[cmp1].length && head2==lstMember[cmp2].length) {
		for (i=0; i<lstMember[cmp1].length+lstMember[cmp2].length; i++) {
			lstMember[parent[cmp1]][i] = rec[i];
		}
		lstMember.pop();
		lstMember.pop();
		cmp1 = cmp1-2;
		cmp2 = cmp2-2;
		head1 = 0;
		head2 = 0;

		//Initialize the rec before performing the new comparison
		if (head1==0 && head2==0) {
			for (i=0; i<namMember.length; i++) {
				rec[i] = 0;
			}
			nrec = 0;
		}
	}

	if (cmp1<0) {
		str = "Question No."+(numQuestion-1)+"<br>"+Math.floor(finishSize*100/totalSize)+"% sorted.";
		document.getElementById("battleNumber").innerHTML = str;

		showResult();
		finishFlag = 1;
	}
	else {
		showImage();
	}
}

//The results+++++++++++++++++++++++++++++++++++++++++++++++
//&#38918;&#20301;=Rank/Grade/Position/Standing/Status
//&#21517;&#21069;=Identification term
function showResult() {
	var ranking = 1;
	var sameRank = 1;
	var str = "";
	var i;

	str += "<table style=\"width:200px; font-size:12px; line-height:120%; margin-left:auto; margin-right:auto; border:1px solid #888888; border-collapse:collapse\" align=\"center\">";
	str += "<tr><td style=\"color:#ffffff; background-color:#888888; text-align:center;\">Rank<\/td><td style=\"color:#ffffff; background-color:#888888; text-align:center;\">Name<\/td><\/tr>";

	for (i=0; i<namMember.length; i++) {
		str += "<tr><td style=\"border:1px solid #888888; width:25px; text-align:right; padding-right:5px;\">"+ranking+"<\/td><td style=\"border:1px solid #888888; width:175px; text-align:center; padding-left:5px;\">"+namMember[lstMember[0][i]]+"<\/td><\/tr>";
		if (i<namMember.length-1) {
			if (equal[lstMember[0][i]]==lstMember[0][i+1]) {
				sameRank++;
			} else {
				ranking += sameRank;
				sameRank = 1;
			}
		}
	}
	str += "<\/table>";

	document.getElementById("resultField").innerHTML = str;
}

//Indicates two elements to compare+++++++++++++++++++++++++++++++++++
function showImage() {
	var str0 = " Question No."+numQuestion+"<br>"+Math.floor(finishSize*100/totalSize)+"% sorted.<br>";
	var str1 = ""+toNameFace(lstMember[cmp1][head1]);
	var str2 = ""+toNameFace(lstMember[cmp2][head2]);

	document.getElementById("battleNumber").innerHTML = str0;
	document.getElementById("leftField").innerHTML = str1;
	document.getElementById("rightField").innerHTML = str2;

	numQuestion++;
}

//Convert numeric value into a name (emoticon)+++++++++++++++++++++++++++++++
function toNameFace(n){
	var str = namMember[n];

	//Exclude the following comment when adding an emoticon
	//Warning not to contradict an indext of namMember
	/*
	str += "<br>&#9472;&#9472;&#9472;&#9472;<br>";
	switch(n) {
		//case -1 Because it is a sample, delete it
		case -1: str+="&#65288; ｴ&#8704;&#65344;&#65289;";break;
		default: str+=""+n;
	}
	*/
	return str;
}
//-->
</script>
<style type="text/css">
<!--
/**********************************************************
 When changing the style of the list, please edit here. 
**********************************************************/
//&#65328;&#12468;&#12471;&#12483;&#12463;=P Gothic
#mainTable{
	font-size: 16px;
	font-family: 'helvetica',sans-serif;
	text-align: center;
	vertical-align: middle;
	width: 410px;
	margin-left: auto;
	margin-right: auto;
	border-collapse: separate;
	border-spacing: 10px 5px;
}
#leftField{
	width: 120px;
	height: 150px;
	border: 1px solid #888888;
}
#rightField{
	width: 120px;
	height: 150px;
	border: 1px solid #888888;
}
.middleField{
	width: 120px;
	height: 70px;
	border: 1px solid #888888;
}
//-->
<!--
A{
  text-decoration : none;
}
-->
<!--
a:hover{color:#99ccff;}
-->
</style>
<style>figure{margin:0}.tmblr-iframe{position:absolute}.tmblr-iframe.hide{display:none}.tmblr-iframe--amp-cta-button{visibility:hidden;position:fixed;bottom:10px;left:50%;transform:translateX(-50%);z-index:100}.tmblr-iframe--amp-cta-button.tmblr-iframe--loaded{visibility:visible;animation:iframe-app-cta-transition .2s ease-out}</style><link rel="stylesheet" media="screen" href="https://assets.tumblr.com/client/prod/standalone/blog-network-npf/index.build.css?_v=6e121b6530ce38be364bf1089290570b"><link rel="stylesheet" type="text/css" href="http://img.shinobi.jp/tadaima/tdftad.css" /><script src="https://assets.tumblr.com/assets/scripts/tumblelog.js?_v=6d92575a6d1cddce7fefd8b949f1b4a4"></script>

<link rel="stylesheet" type="text/css" href="https://assets.tumblr.com/fonts/gibson/stylesheet.css?v=3">

<!-- BEGIN TUMBLR FACEBOOK OPENGRAPH TAGS --><!-- If you'd like to specify your own Open Graph tags, define the og:url and og:title tags in your theme's HTML. --><!-- Read more: http://ogp.me/ --><meta property="fb:app_id" content="48119224995" /><meta property="og:site_name" content="" /><meta property="og:title" content="" /><meta property="og:url" content="http://bias-sorter.tumblr.com/snsd" /><meta property="og:determiner" content="a" /><meta property="og:description" content="" /><meta property="og:type" content="tumblr-feed:entry" /><meta property="og:image" content="http://38.media.tumblr.com/avatar_aeeba2b5692c_512.png" /><meta property="al:ios:url" content="tumblr://x-callback-url/blog?blogName=bias-sorter&amp;postID=" /><meta property="al:ios:app_name" content="Tumblr" /><meta property="al:ios:app_store_id" content="305343404" /><meta property="al:android:url" content="tumblr://x-callback-url/blog?blogName=bias-sorter&amp;postID=" /><meta property="al:android:app_name" content="Tumblr" /><meta property="al:android:package" content="com.tumblr" /><!-- END TUMBLR FACEBOOK OPENGRAPH TAGS -->


<!-- TWITTER TAGS --><meta charset="utf-8"><meta name="twitter:card" content="summary" /><meta name="twitter:title" content="" /><meta name="twitter:description" content="Tumblr Blog" /><meta name="twitter:url" content="" /><meta name="twitter:site" content="tumblr" /><meta name="twitter:app:name:iphone" content="Tumblr" /><meta name="twitter:app:name:ipad" content="Tumblr" /><meta name="twitter:app:name:googleplay" content="Tumblr" /><meta name="twitter:app:id:iphone" content="305343404" /><meta name="twitter:app:id:ipad" content="305343404" /><meta name="twitter:app:id:googleplay" content="com.tumblr" /><meta name="twitter:app:url:iphone" content="tumblr://x-callback-url/blog?blogName=bias-sorter&amp;postID=&amp;referrer=twitter-cards" /><meta name="twitter:app:url:ipad" content="tumblr://x-callback-url/blog?blogName=bias-sorter&amp;postID=&amp;referrer=twitter-cards" /><meta name="twitter:app:url:googleplay" content="tumblr://x-callback-url/blog?blogName=bias-sorter&amp;postID=&amp;referrer=twitter-cards" />

<link rel="alternate" href="android-app://com.tumblr/tumblr/x-callback-url/blog?blogName=ellimists" /><link rel="alternate" href="ios-app://305343404/tumblr/x-callback-url/blog?blogName=ellimists" /><script src="https://assets.tumblr.com/assets/scripts/tumblelog_post_message_queue.js?_v=a8fadfa499d8cb7c3f8eefdf0b1adfdd"></script><link rel="stylesheet" type="text/css" href="https://assets.tumblr.com/fonts/gibson/stylesheet.css?v=3"><link rel="canonical" href="https://ellimists.tumblr.com" /></head>

<body text="#000000" bgcolor="#ffffff" link="#0099ff" vlink="#0099ff" alink="#0099ff">
<table id="mainTable" align="center">
	<tbody><tr>

		<td id="battleNumber" colspan="3" style="padding-bottom: 10px;" style="text-align:center;">Question No.1<br>0% sorted.</td>
	</tr>
	<tr>
		<td id="leftField" onclick="if(finishFlag==0)sortList(-1);" rowspan="2" style="text-align:center;"></td>
		<td class="middleField" onclick="if(finishFlag==0)sortList(0);" style="text-align:center;">

			I Like Both
		</td>

		<td id="rightField" onclick="if(finishFlag==0)sortList(1);" rowspan="2"style="text-align:center;"></td>
	</tr>
	<tr>
		<td class="middleField" onclick="if(finishFlag==0)sortList(0);"style="text-align:center;">
			No Opinion
		</td>

	</tr>
</tbody></table><br><br>
<div id="resultField" style="text-align: center;">
<br><br>
</div>

<script type="text/javascript">
<!--
	initList();
	showImage();
//-->
</script></div>

</div><div><br>
<div align="center">
<a href ="https://animalcrossing.fandom.com/wiki/Villager_list_(New_Horizons)">villager reference</a> / 
<a href="http://ampora.tumblr.com/post/141980407546/sorry-this-has-probably-already-been-asked-i-was">inspiration</a> / <a href="http://infinitexo.weebly.com/ori.html">code credit</a></p>
