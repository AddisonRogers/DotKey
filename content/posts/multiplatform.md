---
title: "Multiplatform"
date: 2023-01-14T19:18:12Z
draft: false
---

## What is Multiplatform
A question that I got quite confused about when started. It is the ability to run the same code base across mutliple platforms. The common pairings are:
- IOS and Android
- Mobile and Desktop
- Mobile and Web
- Mobile, Desktop and Web

## An Introduction
Multiplatform frameworks have gotten a little bit out of hand haven't they?
Between Flutter, React Native and yet another JS library eying for your usage it's a bit difficult to choose.

First a list of the frameworks (At least the ones I know of):
- React Native
- Flutter
- Ionic
- Kotlin Multiplatform Mobile (KMM)
- Native Script
- Maui / Xamarin
- Tauri

I am going to be talking about **all** of them (well aside from tauri as it's in very alpha) and a bit more. I can promise I have not done enough research to make sweeping statements but I will still be making them so take all of this with a grain of salt. But if you are ready..

## A discussion about performance
Generally the frameworks mentioned can be seperated into two groups:

| Webview     | Seperate Engine |
| ----------- | ----------- |
| React Native      | Flutter       |
| Native Script   | Maui / Xamarin        |
| Ionic   |        |

### WebView
The webview group works (generally) by shipping a browser and a communication bridge between the device and the code. Allowing for access to the phone while also being able to use code across platforms. <br/>
However, if you don't need a communication bridge (ie you don't need *easy* access to storage, camera etc) then why not use a Progressive web app (PWA)?. Wrapping a webview with a communication bridge isn't needed when you can just use a webview.

### Seperate Engine
The Seperate Engine group works (even more generalised) by shipping a seperate renderer to the device ie Skia. It should note that dispite a seperate engine, Skia is being used in a lot of places simply because there is little to no difference to native. <br/>
 
## What is 'Native'
Seriously. <br/>
The large issue with all the different multiplatform frameworks is that they largely operate in two distinct ways both of which don't use the exact GUI toolkits for each platform (Compose, Winui etc) but really unless you code natively then you aren't going to use them.. wait what's KMM?

## Kotlin Multiplatform Mobile (KMM)
KMM is the single reason why multiplatform frameworks are so much more confusing than they were like a year ago. It is a way to share the business logic (not ui) across multiple platforms through the JVM machine and Kotlin's ability to compile with LLVM. It allows for the majority of code to be done in Kotlin with the UI done in the device's native toolkits, the best of both worlds?. <br/>
Really though all the different framework's have an ability to switch UI themes depending on the platform you are on so all KMM really brings to the table is allowing Android exclusive apps an easier path to IOS.


## So which one do I use?
TLDR assuming you have the ability to pick up dart you should use Flutter. In nearly every situation it performs and is generally better than the competition. Flutter also gets around the idea that you can't get native looking apps with multiplatform with the cupertino widget set (apple version of the ui tools). <br/>
But that's the easy answer.
```mermaid
flowchart TD
    Start{You want a multiplatform app}
    PerfQ{Do you like JS}
    BridgeQ{Do you want to use the device's capabilites}

    ReactQ{Do you want to make it with React}
    ImmatureQ{Do you prefer more mature frameworks}
    ImmatureFW{Are you okay with Immature frameworks}
    WebsiteWant{Do you want a website}
    AndroidQ{Do you have an android app}
    CORKOTQ{C# or Kotlin}
    


    Start --> PerfQ
    
    PerfQ --Yes--> BridgeQ
    PerfQ --No--> ImmatureFW

    BridgeQ-- No -->PWA
    BridgeQ-- Yes -->ReactQ

    ReactQ-- Yes -->ReactNative(React Native)
    ReactQ-- No -->ImmatureQ

    ImmatureQ-- Yes -->Ionic
    ImmatureQ-- No -->NativeScript(Native Script)

    ImmatureFW --No--> Flutter
    ImmatureFW --Yes--> WebsiteWant

    WebsiteWant --Yes--> Flutter
    WebsiteWant --No--> AndroidQ

    AndroidQ --Yes--> KMM
    AndroidQ --No--> CORKOTQ
    
    CORKOTQ --C#--> MAUI
    CORKOTQ --Kotlin--> KMM
```
There's a bit more than this ie if you hate OOP but all the frameworks have different advantages especially if you know one language more than another or if you have an existing codebase.

<br/>
<br/>

## What about not?
A growing community of people especially ones that dislike the UI not fitting the theme of the OS are wanting for more devs to make programs that are actually specialised to the OS and perfectly fits the user interface, at the end of the day though should we have inclusivity over quality or not.
