# hello-world
test project
/*
 * ATTINY202_LED_BLINK_SMPL1.cpp
 *
 * Created: 2025/03/07 10:27:45
 * Author : todoPapa
 */ 
#include <avr/io.h>
#include <util/delay.h>

//#define F_CPU 20000000UL // CPU Clock = 20MHz (delay.hで定義済み)
#define LED_PIN     PIN2_bm     // PA2にLED接続

int main(void) {
	// クロック設定 20MHz
	_PROTECTED_WRITE(CLKCTRL.MCLKCTRLA, CLKCTRL_CLKSEL_OSC20M_gc); // CLK 20MHz選択
	_PROTECTED_WRITE(CLKCTRL.MCLKCTRLB, 0x00); // 分周なし
	// PA2を出力モードに設定
	PORTA.DIR =LED_PIN;        // IOMAPEDのVPORTAだと、OUTSET,OUTCLRが使えないので…

	while (1) {
		// PA2をHIGHに設定してLED点灯
		PORTA_OUTSET = LED_PIN; 
		_delay_ms(1000);

		// PA2をLOWに設定してLED消灯
		PORTA_OUTSET = LED_PIN; 
		_delay_ms(1000);
	}
}

