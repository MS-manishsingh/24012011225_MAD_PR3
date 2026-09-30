# Practical-3: Implicit & Explicit Intent

**Name:** Manish Kumar Singh
**Enrollment No.:** 24012011225

---

## AIM

To create an **Android application** that demonstrates the use of **Implicit Intent and Explicit Intent**.

The application provides buttons to perform different actions using Android Intents, including making a phone call, opening a URL, viewing the call log, opening the gallery, setting an alarm, opening the camera, and navigating to a Login Activity.

---

# Objectives

The application demonstrates the following Intent-based operations:

1. Make a call to a specific number.
2. Open a specific URL in a browser.
3. Open the Call Log.
4. Open the Gallery.
5. Set an Alarm.
6. Open the Camera.
7. Open a Login Activity.

---

# Features

| No. | Feature             | Intent Type     |
| --: | ------------------- | --------------- |
|   1 | Make Call           | Implicit Intent |
|   2 | Open Specific URL   | Implicit Intent |
|   3 | Open Call Log       | Implicit Intent |
|   4 | Open Gallery        | Implicit Intent |
|   5 | Set Alarm           | Implicit Intent |
|   6 | Open Camera         | Implicit Intent |
|   7 | Open Login Activity | Explicit Intent |

---

# 1. Make Call to Specific Number

The application uses an Intent with the `tel:` URI scheme to initiate a call to a specific phone number.

Example:

```kotlin
val intent = Intent(Intent.ACTION_DIAL)
intent.data = Uri.parse("tel:1234567890")
startActivity(intent)
```

The `tel:` scheme is used to specify the telephone number.

> **Note:** Using `ACTION_DIAL` opens the dialer with the number filled in. Direct calling with `ACTION_CALL` requires the appropriate phone permission.

---

# 2. Open Specific URL

An implicit Intent is used to open a specific website in the user's default browser.

Example:

```kotlin
val intent = Intent(
    Intent.ACTION_VIEW,
    Uri.parse("https://www.google.com")
)
startActivity(intent)
```

The browser capable of handling the URL is selected by Android.

---

# 3. Open Call Log

The Call Log can be opened using an implicit Intent.

Example:

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.type = CallLog.Calls.CONTENT_TYPE
startActivity(intent)
```

The application requests Android to open an application capable of displaying the Call Log.

---

# 4. Open Gallery

The Gallery is opened using an implicit Intent with an image MIME type.

Example:

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.type = "image/*"
startActivity(intent)
```

The `"image/*"` MIME type indicates that the application is requesting image content.

---

# 5. Set Alarm

The application uses an Intent to open Android's alarm functionality.

Example:

```kotlin
val intent = Intent(AlarmClock.ACTION_SET_ALARM)
intent.putExtra(AlarmClock.EXTRA_HOUR, 7)
intent.putExtra(AlarmClock.EXTRA_MINUTES, 30)
startActivity(intent)
```

This demonstrates how an application can communicate with the system's alarm application using an implicit Intent.

---

# 6. Open Camera

The camera can be launched using an implicit Intent.

Example:

```kotlin
val intent = Intent(MediaStore.ACTION_IMAGE_CAPTURE)
startActivity(intent)
```

Android finds an application capable of handling the camera action.

If camera functionality requires runtime permission, the application can check permission using:

```kotlin
ContextCompat.checkSelfPermission()
```

and request it using:

```kotlin
ActivityCompat.requestPermissions()
```

---

# 7. Open Login Activity

An **Explicit Intent** is used to open another Activity within the same application.

Example:

```kotlin
val intent = Intent(this, LoginActivity::class.java)
startActivity(intent)
```

Unlike an implicit Intent, the destination Activity is explicitly specified.

---

# Implicit Intent vs Explicit Intent

## Implicit Intent

An implicit Intent does not specify the exact component that should handle the request.

Android finds a suitable application or component based on the requested action, data, or type.

Example:

```kotlin
Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com"))
```

Examples in this practical:

* Open URL
* Open Call Log
* Open Gallery
* Set Alarm
* Open Camera
* Make Call

---

## Explicit Intent

An explicit Intent specifies the exact Activity or component that should be opened.

Example:

```kotlin
Intent(this, LoginActivity::class.java)
```

In this practical, the Login Activity is opened using an explicit Intent.

---

# Intent Actions Used

The practical demonstrates several Android Intent actions.

| Intent Action                     | Purpose              |
| --------------------------------- | -------------------- |
| `Intent.ACTION_DIAL`              | Opens phone dialer   |
| `Intent.ACTION_VIEW`              | Views/open content   |
| `AlarmClock.ACTION_SET_ALARM`     | Opens alarm creation |
| `MediaStore.ACTION_IMAGE_CAPTURE` | Opens camera         |
| Explicit Intent                   | Opens Login Activity |

---

# Intent.setData()

`setData()` is used to provide a URI to an Intent.

Example:

```kotlin
intent.data = Uri.parse("tel:1234567890")
```

The `Uri.parse()` method converts a string into a URI that can be assigned to the Intent.

Example URL:

```kotlin
Uri.parse("https://www.google.com")
```

Example telephone URI:

```kotlin
Uri.parse("tel:1234567890")
```

---

# Intent.setType()

`setType()` specifies the MIME type of data that an Intent should handle.

Example:

```kotlin
intent.type = "image/*"
```

This indicates that the Intent is working with image files.

The Call Log can also be specified using:

```kotlin
intent.type = CallLog.Calls.CONTENT_TYPE
```

---

# Permissions

Some Android operations require permissions.

Permissions can be declared in the `AndroidManifest.xml`.

Example:

```xml
<uses-permission android:name="android.permission.CALL_PHONE" />
<uses-permission android:name="android.permission.CAMERA" />
```

For permissions that require runtime approval, the application can check permission status using:

```kotlin
ContextCompat.checkSelfPermission()
```

and request permission using:

```kotlin
ActivityCompat.requestPermissions()
```

---

# ActivityResultContracts

Modern Android applications can use **Activity Result APIs** for handling results from Activities and permissions.

Examples include:

```kotlin
ActivityResultContracts.StartActivityForResult()
```

and:

```kotlin
ActivityResultContracts.RequestPermission()
```

These APIs provide a structured way to launch Activities and handle their results.

---

# UI Components

The application uses Android UI components such as:

* `Button`
* `ConstraintLayout`
* `CoordinatorLayout`

Each button performs a different Intent operation.

Example UI structure:

```text
------------------------------------------------
|          IMPLICIT & EXPLICIT INTENT          |
|                                              |
|  [ Make Call ]                               |
|                                              |
|  [ Open URL ]                                |
|                                              |
|  [ Open Call Log ]                           |
|                                              |
|  [ Open Gallery ]                            |
|                                              |
|  [ Set Alarm ]                               |
|                                              |
|  [ Open Camera ]                             |
|                                              |
|  [ Open Login Activity ]                     |
|                                              |
------------------------------------------------
```

---

# Project Structure

```text
Practical-3/
│
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   ├── MainActivity.kt
│           │   └── LoginActivity.kt
│           │
│           ├── res/
│           │   ├── drawable/
│           │   │   └── ...
│           │   │
│           │   └── layout/
│           │       ├── activity_main.xml
│           │       └── activity_login.xml
│           │
│           └── AndroidManifest.xml
│
└── README.md
```

---

# Concepts Studied

The following Android concepts are covered in this practical:

### Intent

An Intent is a messaging object used to request an action from another Android component.

### Types of Intent

* Implicit Intent
* Explicit Intent

### Intent Actions

Different actions can be specified depending on the operation being performed.

### `Intent.setData()`

Used to attach URI data to an Intent.

### `Intent.setType()`

Used to specify the MIME type of the data.

### `Uri.parse()`

Used to convert a string representation into a URI.

### `startActivity()`

Used to launch another Activity or an application component.

### Button

Buttons are used to trigger the different Intent operations.

### ConstraintLayout

Used to design and position UI components.

### CoordinatorLayout

Used as a layout container for coordinating child views.

### Permissions

Required for protected operations such as camera access or direct phone calls.

### `ContextCompat.checkSelfPermission()`

Used to check whether an application has a particular permission.

### `ActivityCompat.requestPermissions()`

Used to request permissions from the user at runtime.

### `ActivityResultContracts`

Used with the Activity Result API to launch Activities and request permissions.

---

# Screenshots

## Main Activity

Add your Main Activity screenshot here:

```markdown
![Main Activity](images/main-activity.png)
```

---

## Make Call

Add your Make Call screenshot here:

```markdown
![Make Call](images/make-call.png)
```

---

## Open URL

Add your browser screenshot here:

```markdown
![Open URL](images/open-url.png)
```

---

## Call Log
