# Converting Images to Flash Memory Icons/images for TFT 
## Softwares
1. [FastStone Photo Resizer](http://www.faststone.org/FSResizerDownload.htm)
2. [LCD image Converter](https://sourceforge.net/projects/lcd-image-converter)
## Steps 1: Resize Image
1. Open FastStone Photo Resizer.
2. Open the image on Left side window.
3. Click on **Add** Option so that image jumps to right side window.
4. Click on **Advanced Option -> Resize based on one side**.
5. Select the **Height** -> and set the pixels according to the display.
6. Select the **Width** -> and set the pixels according to the display.
7. Click on **OK -> Save**
![image](https://github.com/user-attachments/assets/7396d3e5-f062-4a67-ae70-d4f123bfe909)
![image](https://github.com/user-attachments/assets/183aaab7-7b93-4c0d-810e-d2210e128949)
## Steps 2: Convert Image to Numbers!
Once you have the image ready, next step is to convert the image to to hexadecimal. Then we will store it in Arduino Flash Memory.

Remember that their are two options as mentioned earlier:
### Case 1: Monochrome Icons (single colored)
1. Open LCD image Converter.
2. Load the Resized image using **File -> Open**
3. Note down the sixe of the Image ![image](https://github.com/user-attachments/assets/834536fa-acfc-4cda-8921-9c256f17f36a)
4. go to **Options -> Conversion -> Select Preset as Monochrome**
5. go to **Image -> select Block size -> 16bit** (it depends on your Display).
6. Click on **Preview**
7. Copy Everything.
![image](https://github.com/user-attachments/assets/a49cd411-41bf-44d5-80eb-fd41cdf900ac)

### Case 2: Multi Colored Images
1. Open LCD image Converter.
2. Load the Resized image using **File -> Open**
3. Note down the sixe of the Image ![image](https://github.com/user-attachments/assets/834536fa-acfc-4cda-8921-9c256f17f36a)
4. go to **Options -> Conversion -> Select Preset as -> Color R5G6B5** (it depends on your Display color format search it in internet).
5. go to **Image -> select Block size -> 16bit** (it depends on your Display color format search it in internet).
6. Click on **Preview**
7. Copy Everything.
![image](https://github.com/user-attachments/assets/e7e437e0-e3df-4d06-a019-e4f8fb915c0e)

## Step 3: Adding Hex Code to Arduino Code

### Case 2: Multi Colored Images
creat a Header file with name **image.h**
open the file and insert the below code
```
static const uint16_t image_name [] PROGMEM = { // paste the Hex Value here };
```
in the Arduino code:
```
#include <SPI.h> //display
#include <Adafruit_GFX.h>    // Core graphics library
#include <Adafruit_ST7789.h> // Hardware-specific library for ST7789
#include "image.h"

#define TFT_CS   19   // Chip select pin
#define TFT_DC   4  // Data/Command pin
#define TFT_RST  5  // Reset pin (can be set to -1 if not used)

Adafruit_ST7789 tft = Adafruit_ST7789(TFT_CS, TFT_DC, TFT_RST);

void setup() {
tft.init(240, 240, SPI_MODE2);    // Init ST7789 display 240x240 pixels

tft.setRotation(3);
tft.fillRect(0, 0, 240, 240, ST77XX_BLACK); //clearing the display
tft.drawRGBBitmap(x_position, y_position, image_name, image_height, image_width); // replace the x_position, y_position, image_name, image_height, image_width. 
```
