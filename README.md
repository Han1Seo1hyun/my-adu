# my-adu
#include <Adafruit_NeoPixel.h>
#define PIN 6         // 네오픽셀 제어 핀
#define NUMPIXELS 6   // 네오픽셀 LED 개수
Adafruit_NeoPixel pixels(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);
void setup() {
  Serial.begin(9600);
  pixels.begin();            // 네오픽셀 초기화
  pixels.setBrightness(255); // 밝기 설정 (0-255)
}void loop() {
  int a = analogRead(A0);
  Serial.println(a);
  delay(500);
  
  if (Serial.available() > 0) {
    String r = Serial.readString(); // 시리얼 데이터 읽기
    if (r.indexOf('1') == 0) { // 문자 '1'과 비교
        // a가 650 초과일 경우 LED를 끄고, 650 이하일 경우 LED를 켜도록 추가
        if (a > 650) {
          for (int i = 0; i < NUMPIXELS; i++) {
            pixels.setPixelColor(i, pixels.Color(0, 0, 0)); // LED 끄기
          }
          pixels.show(); // 모든 LED 끈 후 한번만 호출
        } else {
          // a가 650 이하일 경우 LED를 켜기
            for (int i = 0; i < NUMPIXELS; i++) {
              pixels.setPixelColor(i, pixels.Color(255, 255, 255)); // 흰색 설정
          }
            pixels.show(); // 모든 LED 설정 후 한번만 호출
        }
    else if (r.indexOf('0') == 0) { // 문자 '0'과 비교
      for (int i = 0; i < NUMPIXELS; i++) {
        pixels.setPixelColor(i, pixels.Color(0, 0, 0)); // LED 끄기
      }
      pixels.show(); // 모든 LED 끈 후 한번만 호출
    }
  }
  // a가 650 초과일 경우 LED를 끄고, 650 이하일 경우 LED를 켜도록 추가
  if (a > 650) {
    for (int i = 0; i < NUMPIXELS; i++) {
      pixels.setPixelColor(i, pixels.Color(0, 0, 0)); // LED 끄기
    }
    pixels.show(); // 모든 LED 끈 후 한번만 호출
  } else {
    // a가 650 이하일 경우 LED를 켜기
    for (int i = 0; i < NUMPIXELS; i++) {
      pixels.setPixelColor(i, pixels.Color(255, 255, 255)); // 흰색 설정
    }
    pixels.show(); // 모든 LED 설정 후 한번만 호출
  }
}
