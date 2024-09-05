---
creation date: 2024-09-05 13:27
modification date: Thursday, 5th September 2024, 13:27:57
tags: 
---
```  

// Invert the CD signal.

// function 194 is the function associated with sdcard_host cd pin

uint8_t value = 0;
value |= (GPIO_SIG194_IN_SEL_V << GPIO_SIG194_IN_SEL_S);
value |= (GPIO_FUNC194_IN_INV_SEL_V << GPIO_FUNC194_IN_INV_SEL_S);
value |= this->m_pinCd & GPIO_FUNC194_IN_SEL_M;
WRITE_PERI_REG(GPIO_FUNC194_IN_SEL_CFG_REG, value);

// Modify slotConfig.gpio_cd and slot_config.gpio_wp if your board has these signals.
sdspi_device_config_t slotConfig = SDSPI_DEVICE_CONFIG_DEFAULT();
slotConfig.host_id = (spi_host_device_t)host.slot;
slotConfig.gpio_cs = (gpio_num_t)this->m_pinCs;
slotConfig.gpio_cd = (gpio_num_t)194;
```