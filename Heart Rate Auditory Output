//OY 8/6/2018 globals
import processing.serial.*;
float value;
Serial myPort;

import ddf.minim.*;
import ddf.minim.ugens.*;

Minim       minim;
AudioOutput out;
Oscil       wave;
AudioSample snare;
float freq = 400;
void setup() {
  size(600, 600);
  printArray(Serial.list());
  String portName = Serial.list()[1];
  myPort = new Serial(this, portName, 115200);
  myPort.bufferUntil(10);
  stroke(0);

  minim = new Minim(this);

  // use the getLineOut method of the Minim object to get an AudioOutput object
  out = minim.getLineOut();

  // create a sine wave Oscil, set to 440 Hz, at 0.5 amplitude
  wave = new Oscil( 440, 0.5f, Waves.SINE );
  // patch the Oscil to the output
  //snare = minim.loadSample("Perc1.mp3", 512);
  wave.patch( out );
  //snare.patch(out);
}
int oldValue = 500;
int minValue = 50;
int maxValue = 200;
void draw() {
  background(255);
  fill(255);  //blank
  rect(0, 200, width, 50);
  fill(60, 255, 0); //green for fill

  float newValue = map(value, 0, 160, 0, width);
  rect(0, 200, newValue, 50);
  textSize(32);
  fill(0); //black for text
  text(value+"", 10, 300);

  //float amp = map( mouseY, 0, height, 1, 0 );
  //wave.setAmplitude( amp );

  //freq = map( value, 0, 1023, 200, 800);
  freq = map( value, 0, 100, 400, 800);
  println("freq: "+freq);
  wave.setFrequency( freq );
  //println(amp, freq);
  //if(oldValue >maxValue && value < minValue){
  //  snare.trigger();
  //}
  //  if(oldValue > minValue && value < maxValue){
  //  snare.trigger();
  //}
  oldValue = (int)value;
}



void serialEvent(Serial myPort) {
  String valString = myPort.readString(); //needs myPort.bufferUntil(10) in setup()
  if (valString != null) {
    valString= trim(valString);
    println(valString);
    try {
      value = int(valString);
      println(value);
    }
    catch(Exception e) {
      println("err");
      value = -1;
    }
  }
}
