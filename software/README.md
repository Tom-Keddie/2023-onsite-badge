# URLs
- Install https://support.arduino.cc/hc/en-us/articles/360019833020-Download-and-install-Arduino-IDE
- ESP8266 https://github.com/esp8266/Arduino#installing-with-boards-manager
- FastLED Doco http://fastled.io/docs/3.1/md__r_e_a_d_m_e.html

# Simple FastLED example
```
#include "FastLED.h"

#define DATA_PIN    2
#define LED_TYPE    WS2812B
#define COLOR_ORDER GRB
#define NUM_LEDS    36
#define BRIGHTNESS  127

CRGB leds[NUM_LEDS];

void setup() {
  delay(3000); // 3 second delay for recovery
  
  // tell FastLED about the LED strip configuration
  FastLED.addLeds<LED_TYPE,DATA_PIN,COLOR_ORDER>(leds, NUM_LEDS)
    .setCorrection(TypicalLEDStrip)
    .setDither(BRIGHTNESS < 255);

  // set master brightness control
  FastLED.setBrightness(BRIGHTNESS);
}


void loop()
{
  static int state = 0;

  switch(state) {
    case 0:
      FastLED.clear(true);
      leds[0] = CRGB::White;
      break;
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
    case 6:
      leds[state-1] = CRGB::Black;
      leds[state] = CRGB::White;
      break;
    case 7:
      leds[state-1] = CRGB::Black;
      leds[state] = CRGB::White;
      leds[state-8+22] = CRGB::White;
      break;
    case 8:
    case 9:
    case 10:
    case 11:
    case 12:
    case 13:
    case 14:
    case 15:
    case 16:
    case 17:
    case 18:
    case 19:
    case 20:
      leds[state-1] = CRGB::Black;
      leds[state-8+22-1] = CRGB::Black;
      leds[state] = CRGB::White;
      leds[state-8+22] = CRGB::White;
      break;
    case 21:
      leds[state-1] = CRGB::Black;
      leds[state-8+22-1] = CRGB::Black;
      leds[state-8+22] = CRGB::White;
      break;      
    default:
      FastLED.clear(true);
      state = -1;
      break;
  }
  
  FastLED.show();  

  delay(100);
  state++;
}
```
