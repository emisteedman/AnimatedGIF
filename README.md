# Use Processing to make an animated GIF
### Step 1: Download and install the `gifAnimation` processing library
Go to [https://github.com/01010101/GifAnimation](https://github.com/01010101/GifAnimation) and download [GifAnimation.zip](https://github.com/01010101/GifAnimation/archive/master.zip). You should now have a folder called `GifAnimation-master.zip` in your downloads folder. It should look similar to this:    
![](GifAnimation1.PNG)    
Extract the folder, rename it as `GifAnimation` and copy it to your Processing library folder. On my Windows PC, the path to my libraries folder is `C:\Users\Art\Documents\Processing\libraries`. Here's a screenshot of the my `GifAnimation` folder in the libraries folder:   
![](GifAnimation2.PNG)
### Step 2: Write a Processing program
Here's the Processing program I'm going to convert to an animated gif. It's an animation of a series of circles:   
  int diameter = 10;
  public void setup()
  {
    size(200,200);
    smooth();
    frameRate(2); //screen is drawn 2 times a second, does not effect speed of gif animation
  }
  public void draw()
  {
    ellipse(100,100,diameter,diameter);
    diameter = diameter + 10;
    println(frameCount);
  }
If you run the program, you'll notice that after `frameCount` reaches 29 or so, the circle is so big that it fills the screen and there is no noticeable change on the screen.
### Step 3: Modify the program to use the `gifAnimation` processing library
Now we are going to add the code that allows us to export the animation as a gif file. The new program is:   
  import gifAnimation.*;
  GifMaker gifExport;

  int diameter = 10;
  public void setup()
  {
    size(200,200);
    gifExport = new GifMaker(this, "test.gif", 100);
    gifExport.setRepeat(0); // make it an "endless" animation
    gifExport.setQuality(255);  // quality range 0 - 255
    smooth();
    frameRate(2); //screen is drawn 2 times a second, does not effect speed of gif animation
  }
  public void draw()
  {
    ellipse(100,100,diameter,diameter);
    diameter = diameter + 10;
    println(frameCount);
    export();
  }
  void export() {
    if(frameCount < 29) {
      gifExport.setDelay(500); //half second delay
      gifExport.addFrame();
    } else {
      gifExport.finish();
      println("gif saved");
      exit();
    }
  }
### Step 4: Find the animated gif in the sketch folder
After you run the modified program, there will no be an animated gif in sketch folder. Here's what mine looked like:   
![](GifAnimation3.PNG)   
Double click on `test.gif` and you should see your animation:   
![](test.gif)    

You can find out more details on the `gifAnimation` library at [https://github.com/01010101/GifAnimation](https://github.com/01010101/GifAnimation) and [https://gist.github.com/jordanorelli/4992290](https://gist.github.com/jordanorelli/4992290). Thanks to Jordan Orelli for creating the library and 01010101 for porting `gifAnimation` for Processing 3.X.

