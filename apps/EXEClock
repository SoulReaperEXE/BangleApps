Graphics.prototype.setFontMichroma36 = function() {
g.setFontCustom(atob("AAAAAAAAAAAAAAAAeAAAAAeAAAAAeAAAAAeAAAAAAAAAAAAAAAAAAAAAAAGAAAAA+AAAAD+AAAAP+AAAA/8AAAD/wAAAf/AAAB/4AAAH/gAAAf+AAAB/4AAAH/gAAAf+AAAAfwAAAAfAAAAAcAAAAAAAAAAAAAAAAAAAAAAAA///AAD///wAH///4AP///8APwAD+APAAAeAeAAAeAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAPAeAAAeAPAAAeAPwAD+AP///8AH///4AD///wAA///AAAAAAAAAAAAAAAAAAAAAEAAAAAOAAAAAfAAAAA+AAAAB8AAAAD8AAAAH4AAAAPwAAAAPgAAAAfAAAAAf///+Af///+Af///+Af///+AAAAAAAAAAAAAAAAAAAAAAAAAA/Af+AD/A/+AH/B/+AP/D/+APwD4eAPADweAfADweAeADweAeADweAeADweAeAHgeAeAHgeAeAHgeAeAHgeAeAHgeAeAHgeAeAHgeAeAHgeAeAHgeAeAHgeAeAPgeAeAPAeAeAPAeAeAPAeAeAPAeAfAPAeAPw/AeAP/+AeAH/+AeAD/8AeAB/wAOAAAAAAAAAAAAAAAAAAAAAAAAAB8APgAD8AP4AH8AP8AP8AP8APgAB+AfAAAeAeAAAeAeAAAPAeAAAPAeAAAPAeAAAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAPAeAeAeAfAeAeAPx/h+AP///+AH///8AD///4AB/h/gAAAAAAAAAAAAAAAAAAAAAAeAAAAA/AAAAA/AAAAB/AAAAD/AAAAH/AAAAPvAAAAPPAAAAfPAAAA+PAAAB8PAAAD4PAAADwPAAAHwPAAAPgPAAAfAPAAA+APAAA8APAAB8APAAD4APAAHwAPAAPgAPAAPAAPAAfAAPAAf///+Af///+Af///+Af///+AAAAPAAAAAPAAAAAPAAAAAPAAAAAOAAAAAAAAAAAAAAAAAAAAAAAAAAf/8PgAf/8P4Af/8P8Af/8P8AeB4A+AeB4AeAeDwAeAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAPAeDwAfAeDwAeAeD4A+AeD+D+AeB//8AeB//4AeA//4AAAP/AAAAAAAAAAAAAAAAAAAAAAAAAAA///AAD///wAH///4AH///8AP4fB+APAeAeAfA8AeAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAfA8APAPA+AeAPgeAeAP8fh+AH8f/8AD8P/8AA8H/4AAAB/gAAAAAAAAAAAAAAAAAAAAAAAAAeAAAAAeAAAAAeAAAAAeAAAAAeAAAAAeAAACAeAAAGAeAAAOAeAAAeAeAAA+AeAAD+AeAAH8AeAAP4AeAAfwAeAA/gAeAB/AAeAD+AAeAP4AAeAfwAAeA/gAAeB/AAAeD+AAAeH8AAAefwAAAe/gAAAf/AAAAf+AAAAf8AAAAf4AAAAfgAAAAfAAAAAAAAAAAAAAAAAAAAAAAAAAMAAB+B/wAD/j/4AH/3/8AP///+AP//A+AfB+AeAeA+AeAeA+APAeA+APAeA+APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA8APAeA+APAeA+APAeA+APAeA+AOAeA+AeAPh/A+AP///+AP/3/8AH/3/8AB/D/wAAAA/AAAAAAAAAAAAAAAAAAAAAAAAAAA/wAAAD/4HAAH/8HwAP/+H4AP5/H8AfAfA8AeAPAeAeAPAeAeAPAeAeAHgfAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHgPAeAHAPAeAPAOAeAPAeAPAPAeAPwfB+AP///8AH///4AD///wAA///AAAAAAAAAAAAAAAAAAAAAAAAAAAB8DwAAB8HwAAB8HwAAB8DwAAAAAAAAAAAAA"), 46, atob("CBIkESMjJCMjIyMjCA=="), 36+(1<<8)+(1<<16));
};
 
var locale = require("locale");
var ENV = process.env;
var W = g.getWidth(), H = g.getHeight();


var current_hr = 0;
var current_psi = 0;
var current_comp = 0;
var current_tmp = 0;
var current_inttmp = 0;
var last_update = 0;

var internal_last_update = -1;
var display_frozen = false;

function getWeatherTemp(){
  try {
    var weather = storage.readJSON('weather.json').weather;
    return locale.temp(weather.temp-273.15);
  } catch(ex) { }

  return "?";
}

function getWeatherHumidity(){
  try {
    var weather = storage.readJSON('weather.json').weather;
    return weather.hum = weather.hum + "%";
  } catch(ex) { }

  return "?";
}

function getWeatherWind(){
  try {
    var weather = storage.readJSON('weather.json').weather;
    var speed = locale.speed(weather.wind).replace("mph", "");
    return Math.round(speed * 1.609344) + "kph";
  } catch(ex) { }

  return "?";
}

function getSteps(){
  try{
    return Bangle.getHealthStatus("day").steps;
  } catch(e) {
    return ">2v12";
  }
}

function getBpm(){
  try{
    return Math.round(Bangle.getHealthStatus("day").bpm) + "bpm";
  } catch(e) {
    return ">2v12";
  }
}

function drawInfo() {
    var current_hr = getBpm();
    var current_psi =  getWeatherHumidity();
    var current_comp = 0;
    var current_tmp = getWeatherTemp();
    var current_inttmp = locale.temp(parseInt(E.getTemperature()));
}

function draw() {
  g.reset().clearRect(0,24,g.getWidth(),g.getHeight());

  var date = new Date();
  g.setFontAlign(0,0);
  g.setFont("Michroma36").drawString(locale.time(date,1), g.getWidth()/2, 56);

  g.setFont("6x8");
  g.drawString(locale.date(new Date(),1), g.getWidth()/2, 80);

  g.setFont("6x8");
  g.drawString("HR", 20, 100);
  g.drawString("PSI", 55, 100);
  g.drawString("Comp", 90, 100);
  g.drawString("Tmp", 125, 100);
  g.drawString("IntTmp", 160, 100);


  if (display_frozen) { g.setColor("#888"); }

  g.setFont("HaxorNarrow7x17");
  g.drawString(""+current_hr, 18, 110);
  g.drawString(""+current_psi, 53, 110);
  g.drawString(""+current_comp, 88, 110);
  g.drawString(""+current_tmp, 123, 110);
  g.drawString(""+current_inttmp, 158, 110);

  }

// init
Bangle.setUI("clock");
require("FontHaxorNarrow7x17").add(Graphics);
g.clear();
Bangle.loadWidgets();
Bangle.drawWidgets();
drawInfo();
draw();

