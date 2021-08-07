---

Title: Activity

Description: Tim White's recent task/project activity

Author: Tim White

Date: 2020-06-25

Robots: noindex,nofollow

Template: content

---

# Recent Activity

The lists below contain tasks I have recently completed. Newly completed tasks are automatically added to the list thanks to the developers over at https://kanboard.org. I use Kanboard for my personal project management and would highly recommend it.

Feel free to skim the list below, or click the header (e.g. "General") to open the board directly to view all tasks in more detail.

---



<div id="tasks-feed">
<script
			  src="https://code.jquery.com/jquery-3.6.0.min.js"
			  integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4="
			  crossorigin="anonymous">
</script>
<script>
function getFeedData(rssurl, index) {
  $.get(rssurl, function(data) {
			publicBoardURLsplit = rssurl.split("/");
			publicBoardURLid = publicBoardURLsplit[publicBoardURLsplit.length -1];
			publicBoardURL = "https://tasks.timwhite.io/public/board/"+publicBoardURLid;
      var $xml = $(data);
      $("#tasks-feed").append('<a target="_blank" href="'+publicBoardURL+'">'+"<h3>"+$($xml.find('title')[0]).text()+"</h3>"+"</a>");

      $xml.find("entry").each(function() {
          var $this = $(this),
              item = {
                  content: $this.find("content").text(),
                  author: $this.find("name").text(),
                  verb: $this.find("content").text().split('"activity-title">')[1].split('<a')[0],
                  date: $this.find("content").text().split('"activity-date">')[1].split('<')[0],
                  task: $this.find("content").text().split('"activity-task-title">')[1].split('<')[0],
                  title: $this.find("title").text(),
                  link: $this.find("reference").text() ,
                }

          if(item.verb.indexOf('closed')>1){
            $("#tasks-feed").append('<div>'+"["+item.date+"]:  "+item.verb + '"'+item.task+'" ' + '<a target="_blank" href="'+item.link+'">'+item.link+'</a>');
          }



      });
  });
}

var publicFeeds = [
  "https://timwhite.io/feed/project/4d5c2b9a77b650f1b6e1146b875ef78af892a0c21a49cf786a3118f8c417",
  "https://timwhite.io/feed/project/7093ddc2d7b06ceee9550ac3ba832614886aaefe662ebb568589212015fc",
	"https://timwhite.io/feed/project/46f9d6b193fb98111c46ce7694b43a241232e35ead7ffa96e6bdeda3b30d",
	"https://timwhite.io/feed/project/5afc469b2bdd7828efd727676c5c78cc90a4b16ce404c9cce8618d49b504"
]

publicFeeds.forEach(getFeedData);

</script>
</div>
