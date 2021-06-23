This is VL6180X distance + ALS sensor. VL6180 works too for this library because it's the same sensor, without the ALS sensor. 
This code uses the same code from Adafruit, because I just rewrote Arduino C++ code to STM32 C code.

This sensor have a very high accuracy for the price. about 1-2mm accuracy between 10-100mm. 

Program example:
```
  #include "main.h"
  #include "VL6180X/VL6180X.h"

  // Structures
  I2C_HandleTypeDef hi2c1;
  
  VL6180X_Init(&hi2c1);

  uint8_t mode = 0;
  /* USER CODE END 2 */

  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
    /* USER CODE END WHILE */
	    float lux = VL6180X_readLux(VL6180X_ALS_GAIN_5);
	    range = VL6180X_readRange();
	    uint8_t status = VL6180X_readRangeStatus();

	    if (status == VL6180X_ERROR_NONE) {
	    	mode = 1;
	    }

	    // Some error occurred, print it out!

	    if  ((status >= VL6180X_ERROR_SYSERR_1) && (status <= VL6180X_ERROR_SYSERR_5)) {
	    	mode = 2;
	    }
	    else if (status == VL6180X_ERROR_ECEFAIL) {
	    	mode = 3;
	    }
	    else if (status == VL6180X_ERROR_NOCONVERGE) {
	    	mode = 4;
	    }
	    else if (status == VL6180X_ERROR_RANGEIGNORE) {
	    	mode = 5;
	    }
	    else if (status == VL6180X_ERROR_SNR) {
	    	mode = 6;
	    }
	    else if (status == VL6180X_ERROR_RAWUFLOW) {
	    	mode = 7;
	    }
	    else if (status == VL6180X_ERROR_RAWOFLOW) {
	    	mode = 8;
	    }
	    else if (status == VL6180X_ERROR_RANGEUFLOW) {
	    	mode = 9;
	    }
	    else if (status == VL6180X_ERROR_RANGEOFLOW) {
	    	mode = 10;
	    }
	    HAL_Delay(50);
  }
```