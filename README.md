This is the Tablet version of the bus ETA web app with larger fonts for display on tablets.

AI 邨巴 巴士 到站時間 Web App

Collect data
Get pictures of 邨巴 Schedule
e.g. 	OceanPointeToTsuenWan.jpg
TsuenWantoOceanPointe.jpg
Get public bus ETA API link
https://cheungbx.github.io/hkbusetaurl/

Create AI  prompt

Use Gemini AI + Canvas to create the web page index.html

Create Github pages to host the web site.
e.g. https://username.github.io/myBusEta/

Set up icon on smart phone

(optional) Hang a tablet on the door to show your bus Schedule









AI Prompt

You are a web application engineer specializing in creating applications that work on publicly hosted web sites that use API to retrieve info from other service providing web sites. 
Produce the fully updated source code, followed by an explanation of changes and code snippets for modified sections.

Release 1.1

Create a web page that searches the Ocean Point private bus schedules to determine the ETA in minutes for the next 3 buses. All times are in HK time zone GMT+8.
Set the HTML Title of the web page to “Bus ETA” followed by the release number. Start with 1.1. and increment the release no each time the code is generated.

Refer to the Bus ETA instructions at the end of this prompt.
Retrieve the lines of bus ETA instructions in this format:
Bus_Co_ID	Route	Direction Stop_name APIUrlOrFilename
where 

Bus_Co_ID is the bus company code - can be 屋苑 KMB CTB GMB
Route is the route number of the bus e.g. 邨巴 234A 52X 
Direction is the direction of the bus e.g. 縉皇居 荃灣 旺角 
Stopname is the first few characters of the station name where the bus will depart from. e.g. 海韻花園 碧堤半島. 
API_UrlOrFilename  is the url for the API link to retrieve the ETA that starts with “https://” (e.g. https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/234A/1) or a filename of the jpg file where the image of the 屋苑 邨巴 schedule can be found.( e.g. TsuenWantoOceanPointe.jpg)

For each line of bus ETA instructions, 
*if APIUrlOrFile does not start with “https://” then it’s a filename. Retrieve the schedules from the jpg file.
**Check the current date to determine which column of bus schedule should be used :  column 1 - Monday to Friday, Column 2 - Saturday, Column 3 - Sunday or Public holiday (dynamically search the Hong Kong government  public holiday web page for the current year to match, do not use static holiday tables for a particular year  ).
** From the target column of bus schedule, calculate the eta in minutes for the next 3 buses as eta1, eta2, eta3

*if UrlOrFile starts with “https://” it is the  API url, 
** send this to the internet API service provider to retrieve the info.
API will returned values  in the following JSON format
{"type":"ETA","version":"1.0","generated_timestamp":"2026-07-30T21:02:13+08:00","data":[{"co":"KMB","route":"234A","dir":"O","service_type":1,"seq":6,"dest_tc":"荃灣西站","dest_sc":"荃湾西站","dest_en":"TSUEN WAN WEST STATION","eta_seq":1,"eta":"2026-07-30T21:06:00+08:00","rmk_tc":"","rmk_sc":"","rmk_en":"","data_timestamp":"2026-07-30T21:01:44+08:00"},{"co":"KMB","route":"234A","dir":"O","service_type":1,"seq":6,"dest_tc":"荃灣西站","dest_sc":"荃湾西站","dest_en":"TSUEN WAN WEST STATION","eta_seq":2,"eta":"2026-07-30T21:31:00+08:00","rmk_tc":"原定班次","rmk_sc":"原定班次","rmk_en":"Scheduled Bus","data_timestamp":"2026-07-30T21:01:44+08:00"},{"co":"KMB","route":"234A","dir":"O","service_type":1,"seq":6,"dest_tc":"荃灣西站","dest_sc":"荃湾西站","dest_en":"TSUEN WAN WEST STATION","eta_seq":3,"eta":"2026-07-30T21:56:00+08:00","rmk_tc":"原定班次","rmk_sc":"原定班次","rmk_en":"Scheduled Bus","data_timestamp":"2026-07-30T21:01:44+08:00"}]}

** Parse the info to retrieve all the ”eta” values (total 3). For each eta, calculate time differences in minutes between the eta time and the current time and store this in eta1, eta2, eta3 respectively.  Ensure proper exception handling when overnight buses ended and the API returned with etas with null values or even no reply. Skip the route if there are no more buses for the current date.

*For each line of API instructions display 
Direction  Route (Blue rectangular background, do not include bus company id in the route , just show the route.)	Stop_name 	eta1 eta2 eta3  (coloured Rectangular background according to eta, if eta < 9 Red, if eta >= 9 <= 15 Orange, if eta > 15 green). 
*if the second or the third eta is null or cannot be found, do not display them.
*Ensure proper exception handling when overnight buses ended and the API returns etas with null values or no response at all  (meaning no more buses for the day) or there are no more buses according to the schedules stored in the image file for 屋苑.

With these info create a web page.
compress the spacing to fit the entire line on a portrait display of a smart phone as follows:
Display the data in a table with columns
.col-dir { width: 24%; font-size: 17.28px; }
.col-route { width: 16%; }
.col-stop { width: 24%; font-size: 15.84px; }
.col-eta { width: 36%; }
If the browser is an IPAD or a Tablet, increase the font size by 50%.

Hidden Autorefresh every 10 seconds (do not show any buttons nor messages about the refresh)

Sample layout of the web page:
縉皇居交通 01-Aug-2026 19:49:00 (current date and time)
開往 路線 發車站 到站時間 (分鐘)
縉皇居 邨巴 荃灣 35 55 75 
… process the rest of the records in the the list of bus API instructions below and produce similar output



List of bus ETA instructions:

屋苑 邨巴 縉皇居 荃灣站 TsuenWantoOceanPointe.jpg
屋苑 邨巴 荃灣 縉皇居 OceanPointeToTsuenWan.jpg
KMB 234A 荃灣 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/234A/1
KMB 234B 荃灣 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/234B/1
KMB 53 荃灣 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/53/1
KMB 234C 觀塘 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/234C/1
KMB 234D 觀塘 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/234D/1
KMB 261B 九龍站 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/261B/1
KMB 48P 火炭 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/48P/1
KMB 52P 旺角 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/52P/1
GMB 96C 荃灣 碧堤半島  https://data.etagmb.gov.hk/eta/route-stop/2008093/2/1
KMB 52X 旺角 海韻花園  https://data.etabus.gov.hk/v1/transport/kmb/eta/ED9E5ACF98190E5C/52X/1
CTB 952 銅鑼灣 海韻花園  https://rt.data.gov.hk/v2/transport/citybus/eta/ctb/002618/952
KMB A38 機場 深井深慈街  https://data.etabus.gov.hk/v1/transport/kmb/eta/5A2A66038B409879/A38/1
KMB 52X 屯門 碧堤半島  https://data.etabus.gov.hk/v1/transport/kmb/eta/B47C12A965D7B481/52X/1
KMB 53 元朗 碧堤半島  https://data.etabus.gov.hk/v1/transport/kmb/eta/B47C12A965D7B481/53/1
CTB 952 屯門 碧堤半島  https://rt.data.gov.hk/v2/transport/citybus/eta/ctb/002619/952

# bus_eta_tablet
