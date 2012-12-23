# Specfications for trueSpeed

    trueSpeed started out as a simple Flash-free web app to find the
 bandwidth speed. This simple app was  a weekend hack.
 However, the app was too simple to be of any good use. The app has
 been morphed into a more useful product to become a better browsing
 bandwidth indicator. 

    trueSpeed is almost all javascript, with a very simple html
  container. It's expected that trueSpeed get's forked off as a
  service, which any body can put in there own page. 


## Basic vistor flow
     The person visiting trueSpeed will be greeted with a world map,
  showing the visitor's location and several servers. The page will
  take a couple of seconds to enable the preferred servers, and a 
  'Start' button will become enabled. Pressing this button will
  initiate sequential or simultaneous download and upload on multiple
  servers. and the results will be shown on the screen. The
  lat-long of client, and speed measured against differ servers will 
  be uploaded to trueSpeed server with a GET query string. This query
  string will also generate a heat map of the world, with the
  previously collected data



## trueSpeed Sponserers / partners
     The partipitating servers will be hosted by sponserers. These
   spnoserers will have to do required CORS setup, and keep some
   sample file, and allow for uploads ( which are to be discraded ). 
   In return, trueSpeed will show there logo on the map, and let user
   click an url to visit the sponsoer site.


## trueSpeed Design
     trueSpeed is a a js module ( with example html5 container ),
     that uses XmlHttpRequest to achieve it's purpose.
     The server data collection is done by parsing the httpd log
     files, and collecting the GET query strings.

### External Libraries
    As trueSpeed is a module, rather than a complete site, it doesn't
    uses any fancy html5/js/css framework or library.
    trueSpeed uses mapstraction to display the world view, and put
    markers. 

### HTML requirements
    / This section will be expanded to become refernce /
    trueSpeed expects three id's
    1. map ==> This shows the map for mapstraction
    2. info ==> This shows status of server on mouseover
    3. result ==> This shows the cumulative result
     
### Javascript details     
     
  The list of servers is provided in server_list. 

  For any server not hosted on the same  machine, CORS setup will be required.


  On page load, the XMLHttpRequests for all the servers are created, and 
  initial connection made to all the servers. Then the markers on the map
  are updated to be either checkmark or cross indicating whether the 
  server is available for testing or not.

  After this initial hand shake, the 'Run' button is enabled.
  If this button is pressed earlier, the state machine can get garbled.

  There is one state machine for each server. The states are:
  * created    <= a new machine
  * connecting <= the XHR is trying to contact server onpage load
  * notfound   <= the server was not found
  * denied     <= CORS setup was not done on server
  * ready      <= ready to start testing
  * downloading<= downloading in progress
  * uploading  <= uploading in progress
  * fnished    <= finished

  
#### Names of Div's

  * 'map' => the map are for mapstraction
  * 'info' => display information about server under cursor
  * 'result' => result display


