[![alt tag](https://github.com/fabian7593/MagicalCamera/blob/master/cameraHighQ.png)](https://github.com/fabian7593/MagicalCamera)

A Magic library to take photos and select pictures in Android. In a simple way and if you need it also save the pictures in device, and facial recognition, get the real uri path or the photo or obtain the private information of the picture.
<br>
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-MagicalCamera-green.svg?style=true)](https://android-arsenal.com/details/1/3623)

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/a64cbf5369e14c3d98f8722c4ad3fad7)](https://www.codacy.com/app/fabian7593/MagicalCamera?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=fabian7593/MagicalCamera&amp;utm_campaign=Badge_Grade)

<br>
##That Offers MagicalCamera.
* **Take picture** with camera device.
* **Select pictures in gallery** device (read in devices). 
* **Write the pictures** that you taken in device, in your own directory.
* Return the **path of your photo** in device. (This issue is solved for @arthursz)
* Working in **android 6.0** (We have a class to request the user permission).
* Create yours **standards of name of pictures**, or use our standard, like "photoname_YYYYmmddHHmmss"
* Posibility of shown the **private info photography**, like latitude, longitude, ISO or others with Exif Class.
* Posibility of **rotate picture** when it's required.
* Select the **quality of the photo** with a percentage, when 1 is the worst and 100 is the better.
* Obtain the LandMark and return a bitmap with a **facial recognition** that you need.
* **Return the Bitmap** Photo if you need to save this in internal DB of your application.
* **Convert your bitmap** in array bytes or string64, if you need to send by Json or XML.

####Other Offers
* A library completely OpenSource.
* Use best practice in POO
* Minimun SDK 14+ API.
* Support library
* Compile with Gradle
* License Under Apache 2.0

<br>
<br>
### If you can do it, buy me a coffee ;)
[![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=L25MKCRPR7TWY)
<br>
<br><br>

## Getting Started

### Download Sources
use git (sourcetree or others)

```bash
git clone https://github.com/fabian7593/MagicalCamera.git
```

Download from [Here](https://github.com/fabian7593/MagicalCamera/zipball/master)

Another type download by Bintray from    [ ![Download](https://api.bintray.com/packages/fabian7593/maven/MagicalCamera/images/download.svg) ](https://bintray.com/fabian7593/maven/MagicalCamera/_latestVersion)
 
 Give me a question in [![Codewake](https://www.codewake.com/badges/ask_question.svg)](https://www.codewake.com/p/magicalcamera)
 
 <br>
## How to use
####Add dependecies
If you need to take photo or select picture, this is your solution.
This library give a magical solution for take a picture,write and red in device, return your uri real path and obtain yhe private info of the photo and facial recognition, you only need to download this and integrate this in your project, maybe downloading it or import in your gradle, like this.

```bash
repositories {
    jcenter()
}

dependencies {
    compile 'com.frosquivel:magicalcamera:4.3'
}
```

If you have any problem with this dependence, because the library override any styles, colors or others, please change the last line for this code:
```bash
 compile('com.frosquivel:magicalcamera:4.3@aar') {
        transitive = false;
    }
```
 
<br>
## What you need?
<br>
###Import library
You need to import the library
```bash
import com.frosquivel.magicalcamera.MagicalCamera;
import com.frosquivel.magicalcamera.Functionallities.PermissionGranted;

//and maybe you need in some ocations
import com.frosquivel.magicalcamera.Objects.MagicalCameraObject;
```
<br>
###Declare Permissions
You need for usage the library in the best way, call any permissions in Android Manifest.xml
If you have android 6.0 the library have a method for validate this permissions, you see this later in this documentation
```bash
 
    //this is for take and select or write the bitmap picture in your device
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.CAMERA"/>
    
    //you need this permission for access the private information and gps locations of yours picture (only if you need this     functionallities)
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    
    //this permission is required only if you use the facial recognition functionallities
    <uses-permission android:name="com.google.android.providers.gsf.permission.READ_GSERVICES" />
    <uses-permission android:name="android.permission.MANAGE_DOCUMENTS"/>
```
Permissions with required user authorization for Androd 6.0, do like this (You need to call this class and method before that you do the instance of MagicalCamera class, you dont have to validate if is only for android 6.0, This class of PermissionGranted already does everything for you, you only need to call this methods)
```bash
        //The parameter this, is the current activity
        PermissionGranted permissionGranted = new PermissionGranted(this);
        
        //permission for take photo, it is false if the user check deny
        permissionGranted.checkCameraPermission();
        
        //for search and write photoss in device internal memory
        //normal or SD memory
        permissionGranted.checkReadExternalPermission();
        permissionGranted.checkWriteExternalPermission();
        
        //permission for location for use the `photo information device.
        permissionGranted.checkLocationPermission();
        
        ...
        //Then instance MagicalCamera
        ...
```

And for activate the Permissions you need to override the method onRequestPermissionsResult in your respective activity or fragment, like this: 
```bash
 @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
    //CALL THIS METHOD EVER IN THIS OVERRIDE FOR ACTIVATE PERMISSIONS
        magicalCamera.permissionGrant(requestCode, permissions, grantResults);
    }
```



<br>
###Declare variable to resize photo ( with pixels percentage )
You need to declare and constant or a simple int variable for the quality of the photo, while greater be, greater be the quality, and otherwise, worst be the quality, like this
```bash
//The pixel percentage is declare like an percentage of 100, if your value is 50, the photo will have the middle quality of your camera. 
// this value could be only 1 to 100.
private int RESIZE_PHOTO_PIXELS_PERCENTAGE = 80;
```

<br>
###Instance Class MagicalCamera
######*YOU NEED TO INSTANCE THIS, AFTER THAT PERMISSION GRANTED INSTANCE.*
You need to instance the MagicalCamera Class, like this:
The fisrt param is the current Activity, and the second the resize percentage photo, and the third param is the Permission Granted
```bash
 MagicalCamera magicalCamera = new MagicalCamera(this,RESIZE_PHOTO_PIXELS_PERCENTAGE, permissionGranted);
 
```

<br>
###Activities Methods
You need to call the methods for take or select pictures in activities that this form:

```bash
//take photo
magicalCamera.takePhoto();

//select picture
magicalCamera.selectedPicture("my_header_name");
```

<br>
###Fragments Methods
You need to call the methods for take or select pictures in fragments that this form:

```bash
//take photo
 if(magicalCamera.takeFragmentPhoto()){
        startActivityForResult(magicalCamera.getIntentFragment(),MagicalCamera.TAKE_PHOTO);
 }
 
 //select picture
 if(magicalCamera.selectedFragmentPicture()){
      startActivityForResult(Intent.createChooser(magicalCamera.getIntentFragment(),  "My Header Example"),
                            MagicalCamera.SELECT_PHOTO);
   }
```

<br>
###Remember override the event onActivityResult
You need to override the method onActivityResult in your activity or fragment like this
```bash
 @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        //CALL THIS METHOD EVER
        magicalCamera.resultPhoto(requestCode, resultCode, data);
        
        //with this form you obtain the bitmap (in this example set this bitmap in image view)
        imageView.setImageBitmap(magicalCamera.getPhoto());
        
        //if you need save your bitmap in device use this method and return the path if you need this
        //You need to send, the bitmap picture, the photo name, the directory name, the picture type, and autoincrement photo name if           //you need this send true, else you have the posibility or realize your standard name for your pictures.
        String path = magicalCamera.savePhotoInMemoryDevice(magicalCamera.getPhoto(),"myPhotoName","myDirectoryName", MagicalCamera.JPEG, true);

       if(path != null){
           Toast.makeText(MainActivity.this, "The photo is save in device, please check this path: " + path, Toast.LENGTH_SHORT).show();
       }else{
           Toast.makeText(MainActivity.this, "Sorry your photo dont write in devide, please contact with fabian7593@gmail and say this error", Toast.LENGTH_SHORT).show();
       }
    }
```

<br>
###The savePhotoInMemoryDevice Method
This method save your bitmap in internal memory device or if the internal memory is full this library save in sdcard (if you have anything :'D)
This method have a lot of params that you can need to use the library:
* **Bitmap:** This is the bitmap that you need to save in memory device.
* **PhotoName:** The name of the photo
* **DirectoryName:** The name of directory that you need to save the image
* **Format:** the format of the photo, maybe png, jpeg or webp. Depends of that you need.
* **AutoIncrementNameByDate:** This variable save the photo with the photo name and the current date and hour. (Only if is true).

For example: myTestMagicalCameraPhoto_20160520131344 -> This is the year 2016, month 5, day 20, hour 13, minute 13 and second 44.

The method:
```bash
 public String savePhotoInMemoryDevice(Bitmap bitmap, String photoName, String directoryName,
 Bitmap.CompressFormat format, boolean autoIncrementNameByDate)
```

<br>
###Types of Formats for save photos
You have any type of formats for save the pictures and the bitmaps.
You can use, the static variables of the library MagicalCamera.
```bash
 Bitmap.CompressFormat jpeg = MagicalCamera.JPEG;
 Bitmap.CompressFormat png = MagicalCamera.PNG;
 Bitmap.CompressFormat webp = MagicalCamera.WEBP;
```

<br>
###Resize photo in real time
You can resize the photo in any moment with this:
```bash
   magicalCamera.setResizePhoto(newResizeInteger);
```

<br>
###Conversion Methods
The library have any methods to convert the bitmap in other formats that you need.
All of this methods are public statics, I mean that you dont have to instance the library for usage this.
You need to call the class * ConvertSimpleImage * And the respective params.
* **bitmapToBytes:** Convert the bitmap to array bytes, only need the bitmap param and the compress format, return array bytes.
* **bytesToBitmap:** Convert the array bytes to bitmap, only need the array bytes in param, return bitmap.
* **bytesToStringBase64:** Convert the array bytes to String base 64, only need the array bytes format in param, return String.
* **stringBase64ToBytes:** Convert string to array bytes, only need the String in param, return array bytes.

<br

### Facial Recognition:

This is a method to return your bitmap (magicalCamera.getPhoto()) like another bitmap with a square draws arround the face of the photo, with the posibillity of modify the color and the stroke of the square. And this is not all, you have the posibility of call the List<Landmark> of the photo with facial recognitions, for save data of all faces, for example the distance between eyes, the nose position and mounth position, all of this is important information for facials recognitions.

You need to write for example:
```bash
if(magicalCamera != null){
    if(magicalCamera.getPhoto() != null){
         //this comment line is the strok 5 and color red for default
         //imageView.setImageBitmap(magicalCamera.faceDetector());
         //you can the posibility of send the square color and the respective stroke
         imageView.setImageBitmap(magicalCamera.faceDetector(50, Color.GREEN));

         List<Landmark> listMark = magicalCamera.getListLandMarkPhoto();
     }else{
         Toast.makeText(MainActivity.this,
                 "Your image is null, please select or take one",
                 Toast.LENGTH_SHORT).show();
     }
 }else{
     Toast.makeText(MainActivity.this,
             "Please initialized magical camera, maybe in static context for use in all activity",
             Toast.LENGTH_SHORT).show();
 }
```

The photo and bitmap converted is like to:
![alt tag](https://github.com/fabian7593/MagicalCamera/blob/master/faceDetection2.png)


### Private information Photo:
This method show you the private information photo if the photo is saved in device or not... 
For view all information the device need to activate GPS locations (and maybe internet), else not show all information :(.

You need to write this code for example:
```bash
 if(magicalCamera.getPhoto()!=null) {
   if(magicalCamera.getImageInformation()) {
 
       StringBuilder builderInformation = new StringBuilder();
 
       if (notNullNotFill(magicalCamera.getLatitude() + ""))
           builderInformation.append("Latitude: " + magicalCamera.getLatitude() + "\n");
 
       if (notNullNotFill(magicalCamera.getLatitudeReference()))
           builderInformation.append("Latitude Reference: " + magicalCamera.getLatitudeReference() + "\n");
 
       if (notNullNotFill(magicalCamera.getLongitude() + ""))
           builderInformation.append("Longitude: " + magicalCamera.getLongitude() + "\n");
 
       if (notNullNotFill(magicalCamera.getLongitudeReference()))
           builderInformation.append("Longitude Reference: " + magicalCamera.getLongitudeReference() + "\n");
 
       if (notNullNotFill(magicalCamera.getDateTimeTakePhoto()))
           builderInformation.append("Date time to photo: " + magicalCamera.getDateTimeTakePhoto() + "\n");
 
       if (notNullNotFill(magicalCamera.getDateStamp()))
           builderInformation.append("Date stamp to photo: " + magicalCamera.getDateStamp() + "\n");
 
       if (notNullNotFill(magicalCamera.getIso()))
           builderInformation.append("ISO: " + magicalCamera.getIso() + "\n");
 
       if (notNullNotFill(magicalCamera.getOrientation()))
           builderInformation.append("Orientation photo: " + magicalCamera.getOrientation() + "\n");
 
       if (notNullNotFill(magicalCamera.getImageLength()))
           builderInformation.append("Image lenght: " + magicalCamera.getImageLength() + "\n");
 
       if (notNullNotFill(magicalCamera.getImageWidth()))
           builderInformation.append("Image Width: " + magicalCamera.getImageWidth() + "\n");
 
       if (notNullNotFill(magicalCamera.getModelDevice()))
           builderInformation.append("Model Device: " + magicalCamera.getModelDevice() + "\n");
 
       if (notNullNotFill(magicalCamera.getMakeCompany()))
           builderInformation.append("Make company: " + magicalCamera.getMakeCompany() + "\n");
 
       new MaterialDialog.Builder(MainActivity.this)
               .title("See photo information")
               .content(builderInformation.toString())
               .positiveText("ok")
               .show();
   }else{
       Toast.makeText(MainActivity.this,
               "You dont have data to show because the real path photo is wrong contact with fabian7593@gmail.com",
               Toast.LENGTH_SHORT).show();
   }
 }else{
   Toast.makeText(MainActivity.this,
           "You dont have data to show because the photo is null (your photo isn't in memory device)",
           Toast.LENGTH_SHORT).show();
 }
 
 
 
 and the method that I use in the example is for validate not null or empty
    private boolean notNullNotFill(String validate){
        if(validate != null){
            if(!validate.trim().equals("")){
                return true;
            }else{
                return false;
            }
        }else{
            return false;
        }
    }
```

See the example of this infomartion return:
![alt tag](https://github.com/fabian7593/MagicalCamera/blob/master/information2.png)

###Rotate image
 The code that you use is in the event override of public void onActivityResult:
```bash
 @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        
        //Please see this line, the last flag is for if camera land scape rotate
        //or false if you dont need to rotate photo
        magicalCamera.resultPhoto(requestCode, resultCode, data, true);
        
        if(magicalCamera.getMyPhoto()!=null) {
            imageView.setImageBitmap(magicalCamera.getMyPhoto());
        }
}
```

##Internal documentation
All the code has a internal documentation for more explanation of this example.

<br><br>
##Preview of Example
![alt tag](https://github.com/fabian7593/MagicalCamera/blob/master/magicalcamera.gif)

<br><br>
##You can see the video explication here (in spanish)
https://www.youtube.com/watch?v=U-JxaFZDSn4

<br><br>
## License
Source code can be found on [github](https://github.com/fabian7593/MagicalCamera)<br>
Licenced under [APACHE 2.0](http://www.apache.org/licenses/LICENSE-2.0).
<br><br>


## About Developer
Developed by [Fabian Rosales]<br>
Known as [Frosquivel Developer]<br>


