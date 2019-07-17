## Introduction:
- In this article we are going to learn how to integrate ***Firebase Push Notification*** in Flutter Application. Firebase provider ***Cloud Messaging Service*** also known as ***Firebase Cloud Messaging (FCM)*** , previously this service is known as ***Google Cloud Messaging (GCM)*** . So don’t get confused with the term, basically FCM is upgraded version of GCM.
- So let’s start integrating FCM in Flutter Application. The plugin which we are required is ***firebase_messaging*** . We need to setup Firebase Project as well.

## Prerequisite (Firebase Project Setup):
- To set up Firebase project, please check my other [article (Setup Firebase Project For Flutter)](https://www.c-sharpcorner.com/article/how-to-do-simple-login-with-email-id-in-flutter-using-google-firebase/) and follow the first 2 steps. ***Please note that you need to follow only the first 2 steps*** .

## Steps:
- Step 1: Follow ***Prerequisite*** and create new flutter project and setup firebase project.

- Step 2: Add firebase_messaging dependency in flutter project. To add dependency open ***pubspec.yaml*** which is located at the root of the project. Check below code snippet for more understanding:
	```
    dependencies:
        flutter:
            sdk: flutter
        cupertino_icons: ^0.1.2
        firebase_messaging: ^5.1.1
    ```
- Step 3: Import ***firebase messaging*** plugin in ***main.dart*** file.
	```
    import 'package:firebase_messaging/firebase_messaging.dart';
    ```
- Step 4: If want to be notified in your app (via onResume and onLaunch, see below) when the user clicks on a notification in the system tray include the following intent-filter within the <activity> tag of your android/app/src/main/AndroidManifest.xml:
	```
    <intent-filter>
      <action android:name="FLUTTER_NOTIFICATION_CLICK" />
      <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
    ```
- Step 5: Following is the instantiation and implementation of firebase push notification in flutter. We have declared _firebaseMessagin object and implemented it’s configuration. 
    ```
    final List<Notification> notifications = [];
    @override
    void initState() {
        super.initState();
        _firebaseMessaging.configure(
            onMessage: (Map<String, dynamic> notification) async {
                setState(() {
                    notifications.add(
                        Notification(
                            title: notification["notification"]["title"],
                            body: notification["notification"]["body"],
                            color: Colors.red,
                        ),
                    );
                });
            },
            onLaunch: (Map<String, dynamic> notification) async {
                setState(() {
                    notifications.add(
                        Notification(
                            title: notification["notification"]["title"],
                            body: notification["notification"]["body"],
                            color: Colors.green,
                        ),
                    );
                });
            },
            onResume: (Map<String, dynamic> notification) async {
                setState(() {
                    notifications.add(
                        Notification(
                            title: notification["notification"]["title"],
                            body: notification["notification"]["body"],
                            color: Colors.blue,
                        ),
                    );
                });
            },
        );

-   Firebase Messaging configuration includes events like onMessage, onResume, onLanch.
    - ***onMessage***: If app is open and notification will be delivered then this event will be fired.
    - ***onResume***: If app is in background and notification will be delivered and you will open the app from notification tap then this event will be fired.
    - ***onLaunch***: If app is close and notification will be delivered and you will open the app from notification tap then this event will be fired.

- Step 6: Request notification permission.
	```
    _firebaseMessaging.requestNotificationPermissions();
    ```
- Step 7: Send Firebase Push Notification from Firebase Project. Go to Firebase project and click on ***Cloud Messaging*** option in left menu under Grow Option. You can create you first Notification from there. 
- ***NOTE THAT*** : You need to pass ***click_action*** and ***FLUTTER_NOTIFICATION_CLICK*** in additional option custom data.


- Try sending notification while 1. Your App is Open 2. While Your App is in Background and 3. While Your App is Closed. That’s all you are done with Flutter Firebase Push Notification.

- ***I have attached full source code and git repository for this article*** .

## Conclusion:
In this article we have learned how to integrate firebase push notification in flutter app and broadcast push notification from firebase. You can also broadcast push notification programmatically from server side.
