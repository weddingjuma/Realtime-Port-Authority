Documentation
=============


[BusTime Developer API Guide 2.4.pdf](https://github.com/epicmeowsni/Realtime-Port-Authority/blob/master/Documentation/BusTime%20Developer%20API%20Guide%202.4.pdf) is the API guide to the Real-Time Tracking of Port Authority.

Google's [General Transit Reference Specification](https://developers.google.com/transit/gtfs/reference) is also an important read.

The file given by Port Authority is [here](http://www.portauthority.org/GeneralTransitFeed/) but this is only for taking note of stops and whatnot.

[Google Maps API](https://developers.google.com/maps/)

##For Developers

Make sure you get your API key... You must first make an account in http://realtime.portauthority.com,
go to My Account, then request for an API Key.

Looks like in order for this to go commercially, we would have to request
for a commercial API key. But we will have to prove a real working version
of the app.

Ritwik figured out how the API works... It's a simple hyperlink provided in the API

For example... to get all P3 buses running... (will not work without your API copy pasted into "your_key"):
http://realtime.portauthority.org/bustime/api/v1/getvehicles?key=your_key&rt=P3

This will return an XML of the real-time data.... with some data changed

```
<bustime-response>
	<vehicle>
		<vid>3247</vid>
		<tmstmp>20140729 16:06</tmstmp>
		<lat>0</lat>
		<lon>9001</lon>
		<hdg>159</hdg>
		<pid>801</pid>
		<rt>P3</rt>
		<des>blablah</des>
		<pdist>35442</pdist>
		<spd>27</spd>
		<tablockid>P3 -335</tablockid>
		<tatripid>53191</tatripid>
		<zone/>
	</vehicle>
	<vehicle>
	.
	.
	.
	etc...
```
This data changes every 10 seconds!

Apparently printing your current location in Google maps is done through
```
map.setMyLocationEnabled(true);
```

Apparently a hunky dunky way of [displaying points](http://stackoverflow.com/questions/14822567/display-many-points-with-google-maps-android-api-v2) on the screen is through
...Through android


```
mMap.setOnCameraChangeListener(new OnCameraChangeListener() {
   @Override
   public void onCameraChange(CameraPosition position) {
      final LatLngBounds screenBounds = mMapView.getProjection().getVisibleRegion().latLngBounds;
      for (YourPoint point : mPoints) {
         if (screenBounds.contains(point.getLatLng()) {
            mMapView.addMarker(point.getLatLng()); //over here....
         }
      } 
   }
}
```
This means atm, we can just get a map and input coordinates to print the location of each bus that we can pull up.

So then... TODOS as of 07.29.2014:
- Know Android programming (java, xml, manifest files...)
- Figure out Google Maps API
- ~~print locations of the buses that we poll.~~ done by Ritwik

#Installing Android Studio on Ubuntu (and Linux in general)

It seems hard but it really isn't... not really... But there are some quirks

######Prequisites:
- [Oracle Java 7](http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html)
- [32-Bit Libraries](http://askubuntu.com/questions/454253/how-to-run-android-sdk-in-ubuntu-64-bits)

######Instructions:
1. Install Oracle Java 7 (might as well install 8 also if you want)
	- `sudo add-apt-repository ppa:webupd8team/java`
	- `sudo apt-get update`
	- `sudo apt-get install oracle-java7-installer`
		- note... oracle-java8-installer works too...
		- but make sure oracle java7 is the main one...
		- Take note that java 8 and android isn't happening in the near future... yet...
2. Install 32-bit libraries
	- `sudo dpkg --add-architecture i386`
	- `sudo apt-get update`
	- `sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386`
3. Install Android Studio..
	- `sudo add-apt-repository ppa:paolorotolo/android-studio`
	- `sudo apt-get update`
	- `sudo apt-get install android-studio`
4. Install the update that pops up (would be 0.8.2)
5. Install the SDK Manager and install
	- to 4.2.2
	- Google Play Services
	- Google Repositories
	- ... pretty much everything kinda a little
	
######Opening the Project here....
- Click on Import Project (sometimes in the File dropdown menu)
- go all the way up to *../Realtime-Port-Authority/Android*
- click on the android there

After this... should be good...