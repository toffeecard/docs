---
sidebar_position: 3
---
# User Linking
This section describes how to implement and use the User Linking. When a user clicks on the link from a game, the link automatically associates the user’s ID with the app. If the app is not installed, the user is redirected to the appropriate app store (Google Play Store or Apple App Store). After installation (or immediately if already installed), the specified user ID is linked to the user in the app.

## Overview
```
https://link.toffeecard.com?game_id=<game_id>&user_id=<user_id>&user_type=[user_type]
```
* **game_id (required)**: Unique identifier for the game.
* **user_id (required)**: Unique identifier for the user in the context of the game.
* **user_type (optional)**: A parameter indicating the type of user (e.g., `new`, `vip`, or any other categorization relevant to your game). 

When a user clicks the link:
1. **Check if the app is installed.**
* If installed, the app opens directly and links the user automatically based on the `user_id`.
* If not installed, the user is redirected to the store page (App Store or Google Play) to download the app.
2. **After installation  the user is linked automatically** based on the `user_id` included in the link.

## How It Works
1. **User taps the link in the game.**
2. **Deep Link / App Store redirection:**
* The link attempts to open the app.
* If the app is **not installed**, the system redirects the user to the store page:
  * **iOS** → Apple App Store
  * **Android** → Google Play Store
3. **App receives the link (with all parameters).**
4. **Application logic links user** using the `user_id` (and optionally `user_type`).

## Integration Steps
1. **Construct the URL** with the appropriate query parameters:
```
https://link.toffeecard.com?game_id=12345&user_id=abc123&user_type=vip
```
* Replace `12345` with your actual `game_id`.
* Replace `abc123` with the actual `user_id`.
* Optional: Replace `vip` with your desired `user_type` (or omit `user_type` entirely if not needed).

2. Provide this URL within your game wherever you want to trigger the user linking:
* Buttons
* In-game messages
* Promotional banners


## Example
1. **User sees a prompt** in Game A.
2. The banner in Game A points to:
```
https://link.toffeecard.com?game_id=SUPERGAME&user_id=123456
```
3. When the user taps the button:
  1. If ToffeeCard is installed, **the app opens immediately** with game_id=SUPERGAME and user_id=123456.
  2. If ToffeeCard is **not** installed, the user is taken to the app store to download it. Once they open the app for the first time, the link is processed, and the user is recognized as 123456 from SUPERGAME.