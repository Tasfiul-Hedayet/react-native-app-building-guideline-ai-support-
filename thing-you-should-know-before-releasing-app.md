6# Prompt Part - 

## If you build a existing app use this technique- 

* go to play store > choose the app you like 
* copy the description including the features 
* then paste it to chatgpt/deepseek to generate 
  a prompt based on your given description using 
  react native cli. 

+ add 3 extra pages - 

- about page 
( Tasfiul Hedayet
Version: 1.0.0
Made with ❤️
in Bangladesh ) 

- changelog page (with version)

- system page (system, dark, light)

# After build the apk - 

- run testing for the app before releasing the apk.
- run smoke test for finding bugs and issues. if satisfied, then release the apk.


# Releasing the apk (things you should know)

1. For apk build only Release apk for small size and user friendly. Don't use the debug apk, 
bcuz it's large in size and it's including Debugging console. (Only for developers)

2. Use react native reanimated for animation 

3. Release only the arm-64-v8a for android, don't build the rest 3. 
Bcuz they're for old phones and emulators. (Only build 4 of them when Releaseing on play store)

4. Allocate 2GB ram when releasing the apk for faster build

# if you're using vps (for my system)

## Download from vps 
## easiest way 
* tap on the apk file
* it will selected > then click on the 3 dots > download
* it will directly download as a apk file in your phone
  
## another way 
* open in termux 
* cp app.apk app.apk.zip 
* termux-share app.apk.zip 
* open with rar app 
* select send option 
* dm someone in telegram 
* download the file in telegram
* remove .zip and it converted to .apk automatically 
* install it
