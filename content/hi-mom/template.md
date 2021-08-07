
<div>
 <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>


<span>Step 1: Enter Data</span><br><br>

<label for="header-img-url">Header Image URL:</label><br><input type="text" id="header-img-url" name="header-img-url"><br><br>

<label for="footer-img-url">Footer Image URL:</label><br><input type="text" id="footer-img-url" name="header-img-url"><br><br>

<label for="template-title">Title:</label><br><input type="text" id="template-title" name="header-img-url"><br><br>

<label for="template-tagline-1">Tagline 1:</label><br><input type="text" id="template-tagline-1" name="header-img-url"><br><br>

<label for="template-tagline-2">Tagline 2:</label><br><input type="text" id="template-tagline-2" name="header-img-url"><br><br>

<label for="template-tagline-3">Tagline 3:</label><br><input type="text" id="template-tagline-3" name="header-img-url"><br><br>

<span>Step 2: </span><button type="button" id="populate">Populate Template</button>


<br><br>
<textarea id="template" name="template" rows="4" cols="50">
Enter form data above and click "Populate template" to see results!
</textarea>
<br><br>
<span>Step 3: </span><button type="button" id="save-as-html">Save as .html file</button>

<script>

$( "#populate" ).click(function() {

var a = $("template-title").text();
var b = $("template-tagline-1").text();
var c = $("template-tagline-2").text();
var d = $("template-tagline-3").text();
var e = $("header-img-url").text();
var f = $("footer-img-url").text();
var g = '<!--[if mso]><style type="text/css">body, table, td {font-family: Arial, Helvetica, sans-serif !important;}</style><![endif]-->';

  var doc = `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"> <html lang="en"> <!-- header including title and global-CSS --> <head>   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">   <meta name="viewport" content="width=device-width, initial-scale=1">   <meta http-equiv="X-UA-Compatible" content="IE=edge">   <!-- Title -->   <title>${a}</title>   <!-- email-wide Style -->   <style type="text/css">  /* Base Element Styling */  html { font-family: "Arial", sans-serif;  }  /* CLIENT-SPECIFIC STYLES */  body, table, td, a { -webkit-text-size-adjust: 100%; -ms-text-size-adjust: 100%; }  table, td { mso-table-lspace: 0pt; mso-table-rspace: 0pt; }  img { -ms-interpolation-mode: bicubic; }  /* RESET STYLES */  img { border: 0; outline: none; text-decoration: none; }  table { border-collapse: collapse !important; }  body { margin: 0 !important; padding: 0 !important; width: 100% !important; }  h1, h2, h3, h4, h5 { color: #46296e; }  body>center * { max-width: 1200px; }  /* iOS BLUE LINKS */  a[x-apple-data-detectors] { color: inherit !important; text-decoration: none !important; font-size: inherit !important; font-family: inherit !important; font-weight: inherit !important; line-height: inherit !important;  }  /* ANDROID CENTER FIX */  div[style*="margin: 16px 0;"] { margin: 0 !important; }  /* MEDIA QUERIES */  /* @media all and (max-width:639px){ .wrapper{ width:320px!important; padding: 0 !important; } .container{ width:300px!important;  padding: 0 !important; } .mobile{ width:300px!important; display:block!important; padding: 0 !important; } .img{ width:100% !important; height:auto !important; } *[class="mobileOff"] { width: 0px !important; display: none !important; } *[class*="mobileOn"] { display: block !important; max-height:none !important; }  } */   </style> </head> <body style="margin:0; padding:0; background-color: #eeeeee">   <!-- Tagline template -->   <div style="display: none; font-size: 0px; line-height: 0px; max-height: 0px; max-width: 0px; width: 0px; opacity: 0; overflow: hidden;">${b}<p>&nbsp;  ${c}<p>&nbsp;${d}`


  var doc2 = `</div>  ${g}   <!-- no idea what this is, ignore -->   <span style="display: block; width: 640px !important; max-width: 640px; height: 1px" class="mobileOff"></span>   <center>  <!-- "Main Table" -->  <table width="100%" style="max-width:1200px; Margin:auto" border="0" cellpadding="0" cellspacing="0"> <tr>   <td align="left" valign="top">  <!-- "Main Table - row 1" devoted exclusively to banner image -->  <table width="100%" cellpadding="0" cellspacing="0" border="0" class="wrapper" bgcolor="#FFFFFF"> <!-- ignore this --> <tr>   <td height="10" style="font-size:10px; line-height:10px;">&nbsp;</td> </tr> <tr>   <td align="center" valign="top"> <img src="${e}" width="100%" style="margin:0; padding:0; border:none; display:block;" border="0"/>   </td> </tr> <!-- ignore this --> <tr>   <td height="10" style="font-size:10px; line-height:10px;">&nbsp;</td> </tr>  </table>  <!-- "Main Table - row 2" devoted to your custom content -->  <table width="100%" cellpadding="0" cellspacing="0" border="0" class="wrapper" bgcolor="#FFFFFF"> <tr>   <td height="10" style="font-size:10px; line-height:10px;">&nbsp;</td> </tr> <tr>   <td align="center" valign="top">  <table width="80%" cellpadding="0" cellspacing="0" border="0" class="container"> <tr>   <td width="80%" class="mobile" align="left" valign="top"> <span style="font-family: Arial, sans-serif !important;">   [Insert your content here] </span>   </td> </tr>  </table>   </td> </tr> <tr>   <td height="10" style="font-size:10px; line-height:50px;">&nbsp;</td> </tr>  </table>  <!-- "Main Table - row 3" devoted to your footer -->  <table width="100%" cellpadding="0" cellspacing="0" border="0" class="wrapper" bgcolor="#FFFFFF"> <tr>   <td height="10" style="font-size:10px; line-height:10px;">&nbsp;</td> </tr> <tr>   <td align="center" valign="top">  <table width="100%" cellpadding="0" cellspacing="0" border="0" class="container"> <tr>   <td align="center" valign="top"> <a href="#"><img src="${f}" width="100%" style="margin:0; padding:0; border:none; display:block;" border="0" alt="" /></a>   </td> </tr>  </table>  <table width="100%" cellpadding="0" cellspacing="0" border="0" class="container"> <tr>   <td align="center" valign="top"> <img src="https://premier-research.com/wp-content/uploads/2020/04/footer-logo-01.png" width="100%" style="margin:0; padding:0; border:none; display:block;" border="0" alt="" />   </td> </tr>  </table>   </td> </tr> <tr>   <td height="10" style="font-size:10px; line-height:10px;">&nbsp;</td> </tr>  </table>   </td> </tr>  </table>   </center> </body> </html>`;
$('#template').val(doc);



});







</script>

</div>
