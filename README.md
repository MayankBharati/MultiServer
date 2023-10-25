# AndroidWebServer: Empower Your Android App with a Built-In Web Server

[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-WebServer-lightgrey.svg?style=flat)](https://android-arsenal.com/details/1/2847)
[![Platform](https://img.shields.io/badge/platform-android-green.svg)](http://developer.android.com/index.html)
[![API](https://img.shields.io/badge/API-8%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=8)
[![Twitter](https://img.shields.io/badge/Twitter-@LopezMikhael-blue.svg?style=flat)](http://twitter.com/lopezmikhael)

Introducing AndroidWebServer, an exceptional sample project that equips your Android application with a seamless **Web Server** using the [NanoHTTPD](https://github.com/NanoHttpd/nanohttpd) library.

## How to Utilize AndroidWebServer

1. To integrate this **Android Web Server** into your project, follow these simple steps:

   - Add the [NanoHTTPD](https://github.com/NanoHttpd/nanohttpd) library as a dependency in your build.gradle file:

     ```groovy
     compile 'org.nanohttpd:nanohttpd:2.2.0'
     ```

   - Then, create your **Android Web Server** class. Here's an example:

     ```java
     public class AndroidWebServer extends NanoHTTPD {
     
         public AndroidWebServer(int port) {
             super(port);
         }
     
         public AndroidWebServer(String hostname, int port) {
             super(hostname, port);
         }
         
         //...
     }
     ```

3. Add a `serve()` method to your **Android Web Server** class:

   ```java
   @Override
   public Response serve(IHTTPSession session) {
       String msg = "<html><body><h1>Hello server</h1>\n";
       Map<String, String> parms = session.getParms();
       if (parms.get("username") == null) {
           msg += "<form action='?' method='get'>\n";
           msg += "<p>Your name: <input type='text' name='username'></p>\n";
           msg += "</form>\n";
       } else {
           msg += "<p>Hello, " + parms.get("username") + "!</p>";
       }
       return newFixedLengthResponse( msg + "</body></html>\n" );
   }
   ```

   The `serve()` method is critical because it defines the response sent by your web server.

4. You can now instantiate and start your server in your activity. (Full implementation can be found [**here**](/app/src/main/java/com/mikhaellopez/androidwebserver/MainActivity.java))

   ```java
   AndroidWebServer androidWebServer = new AndroidWebServer(port);
   androidWebServer.start();
   ```

   To stop the server:

   ```java
   androidWebServer.stop();
   ```

## Licensing

**AndroidWebServer**, created by [Lopez Mikhael](http://mikhaellopez.com/), operates under the [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0). Elevate your Android app with this valuable Web Server tool while adhering to open-source principles.
