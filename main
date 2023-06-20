#include <EEPROM.h> //library

// Alamat EEPROM untuk menyimpan waktu lampu
const int alamatWaktuOn = 0;
const int alamatWaktuOff = 4;

// Pin yang digunakan untuk mengendalikan lampu
//jika memakai nodemcu
const int lampuPagar = D1;
const int lampuRtamu = D2;
const int lampuKmrAts = D3;
const int lampuKmrBwh = D4;

/* jika memakai arduino dan nano
const int lampuPagar = 13;
const int lampuRtamu = 14;
const int lampuKmrAts = 15;
const int lampuKmrBwh = 16; */

// Waktu lampu dinyalakan (06:00 PM)
const unsigned long waktuOn = 18 * 60 * 60 * 1000;

// Waktu lampu dimatikan (06:00 AM)
const unsigned long waktuOff = 6 * 60 * 60 * 1000;

void setup() {
  pinMode(lampuPagar, OUTPUT);  // Mengatur pin lampu sebagai OUTPUT
  pinMode(lampuRtamu, OUTPUT);  // Mengatur pin lampu sebagai OUTPUT
  pinMode(lampuKmrAts, OUTPUT);  // Mengatur pin lampu sebagai OUTPUT
  pinMode(lampuKmrBwh, OUTPUT);  // Mengatur pin lampu sebagai OUTPUT

  Serial.begin(9600);  // Memulai koneksi serial

  unsigned long waktuOnSaved = EEPROMReadLong(alamatWaktuOn);  // Membaca waktu dari EEPROM
  unsigned long waktuOffSaved = EEPROMReadLong(alamatWaktuOff);

  // Jika waktu di EEPROM tidak valid, simpan waktu default
  if (waktuOnSaved == 0xFFFFFFFF || waktuOffSaved == 0xFFFFFFFF) {
    EEPROMWriteLong(alamatWaktuOn, waktuOn);
    EEPROMWriteLong(alamatWaktuOff, waktuOff);
  }
}

void loop() {
  unsigned long sekarang = millis();  // Mendapatkan waktu saat ini menggunakan millis()

  unsigned long waktuOnSaved = EEPROMReadLong(alamatWaktuOn);  // Membaca waktu dari EEPROM
  unsigned long waktuOffSaved = EEPROMReadLong(alamatWaktuOff);

  // Memeriksa apakah lampu harus dinyalakan atau dimatikan
  if (sekarang >= waktuOnSaved && sekarang < waktuOffSaved) {
    digitalWrite(lampuPagar, HIGH);  // Menyalakan lampu
  } else {
    digitalWrite(lampuPagar, LOW);  // Mematikan lampu
  }

  delay(1000);  // Menunda selama 1 detik sebelum memeriksa waktu lagi
    // Memeriksa apakah lampu harus dinyalakan atau dimatikan
  if (sekarang >= waktuOnSaved && sekarang < waktuOffSaved) {
    digitalWrite(lampuRtamu, HIGH);  // Menyalakan lampu
  } else {
    digitalWrite(lampuRtamu, LOW);  // Mematikan lampu
  }

  delay(1000);  // Menunda selama 1 detik sebelum memeriksa waktu lagi
    // Memeriksa apakah lampu harus dinyalakan atau dimatikan
  if (sekarang >= waktuOnSaved && sekarang < waktuOffSaved) {
    digitalWrite(lampuKmrAts, HIGH);  // Menyalakan lampu
  } else {
    digitalWrite(lampuKmrAts, LOW);  // Mematikan lampu
  }

  delay(1000);  // Menunda selama 1 detik sebelum memeriksa waktu lagi
    // Memeriksa apakah lampu harus dinyalakan atau dimatikan
  if (sekarang >= waktuOnSaved && sekarang < waktuOffSaved) {
    digitalWrite(lampuKmrBwh, HIGH);  // Menyalakan lampu
  } else {
    digitalWrite(lampuKmrBwh, LOW);  // Mematikan lampu
  }

  delay(1000);  // Menunda selama 1 detik sebelum memeriksa waktu lagi
}

unsigned long EEPROMReadLong(int address) {
  unsigned long value = 0;
  for (int i = 0; i < 4; i++) {
    value <<= 8;
    value |= EEPROM.read(address + i);
  }
  return value;
}

void EEPROMWriteLong(int address, unsigned long value) {
  for (int i = 3; i >= 0; i--) {
    EEPROM.write(address + i, (value >> (i * 8)) & 0xFF);
  }
}
