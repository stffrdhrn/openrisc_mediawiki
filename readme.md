# opencores wiki backup

This is a backup of the old media wiki found on opencores. 

The goal is to slowly migrate the content to openrisc.io and other places. 

This is just the current version of the pages and not the history.  History can 
be extracted using http://opencores.org/or1k/Special:Export, but I didnt think
its needed

# Backup steps

See the [media wiki index.php](https://www.mediawiki.org/wiki/Manual:Parameters_to_index.php) 
page for more details on what you can pull from media wiki.

```bash
 # Backup the all pages special page
 curl http://opencores.org/or1k/Special:AllPages  -o opencores-allpages
 
 # extract the actual page links
 grep  -o 'a href=\"/or1k/[^\"]\+' opencores-allpages | cut -d\/ -f3 > opencores-pages.txt
 
 # for each page download and save the page from opencores
 cat opencores-pages.txt | while read page; do 
  curl http://opencores.org/or1k/${page}?action=raw -o $page.raw
 done
```
