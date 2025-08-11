
# Tutorial Xiaomi AX3200 OpenWRT

## Panoramica

Una raccolta di tutorial per sbloccare, installare OpenWRT e recuperare il router Xiaomi AX3200.

## Hardware Testato

| Dispositivo           | Versione Sistema         | Modello |
| --------------------- | ----------------------- | ------- |
| Xiaomi Router AX3200  | MiWiFi Release 1.0.83   | RB01    |

## Tutorial: Installazione di OpenWRT

**Nota:** Si consiglia di ripristinare le impostazioni di fabbrica e di effettuare una configurazione basilare tramite router.miwifi.com prima di procedere.

1. Scarica ed estrai [xmir-patcher](https://github.com/openwrt-xiaomi/xmir-patcher).
2. Scarica l’ultimo firmware OpenWRT stabile da [qui](https://openwrt.org/toh/xiaomi/ax3200) e salvalo nella cartella "firmware" di xmir-patcher.

Avvia l’applicazione e segui questi passaggi nell’ordine indicato (procedi solo se ogni step ha successo):

- Set IP address
- Connect to device (install exploit) → apparirà il messaggio "SSH server are activated!"
- Install permanent SSH
- Install firmware (from directory "firmware")

Il router si riavvierà automaticamente con OpenWRT.

## Fix post-installazione per softbrick dopo 6 riavvii (LED arancione lampeggiante)

Dopo l’installazione, esegui questi comandi via SSH per prevenire il softbrick causato dai nuovi bootloader:

```sh
fw_setenv boot_fw1 "run boot_rd_img;bootm"
fw_setenv flag_try_sys1_failed 8
fw_setenv flag_try_sys2_failed 8
fw_setenv flag_boot_rootfs 0
fw_setenv flag_boot_success 1
fw_setenv flag_last_success 1
```

Riavvia il router e verifica con `fw_printenv` che “flag_try_sys1_failed” abbia valore 8 o superiore. Se sì, il fix è stato applicato correttamente.

## Unbrick

1. Avvia MIWIFIRepairTool.x86.
2. Seleziona il firmware stock da flashare nel primo campo, lascia il resto invariato.
3. Premi il pulsante in basso a destra.
4. Seleziona "Ethernet".
5. Premi il secondo pulsante in basso a destra.
6. Collega il cavo RJ45 alla porta WAN del router e al PC, tieni premuto il reset mentre ricolleghi l’alimentazione, rilascia il tasto quando il LED arancione lampeggia velocemente.
7. Il tool effettuerà il flash; al termine, il LED power lampeggerà velocemente di blu.
8. Stacca e riattacca l’alimentazione per la prima configurazione con firmware stock.

**Nota:**  
- Può essere utile impostare un IP statico (192.168.31.100) sull’interfaccia ethernet.  
- In alcuni casi, può esser utile collegare il cavo alla prima porta LAN invece della WAN.

## Link utili

- [info](https://github.com/mikeeq/xiaomi_ax3200_openwrt)
- [tutorial unbrick](https://www.youtube.com/watch?v=BoIQ4cNWR-Y)
- [xmir patcher fork (backup)](https://github.com/Razorbacktrack/xmir-patcher)

---

# Tutorial Xiaomi AX3200 OpenWRT

## Overview

A collection of tutorials for unlocking, installing OpenWRT, and recovering the Xiaomi AX3200 router.

## Tested Hardware

| Device                | System Version          | Model  |
| --------------------- | ---------------------- | ------ |
| Xiaomi Router AX3200  | MiWiFi Release 1.0.83  | RB01   |

## How to Install OpenWRT

**Note:** It is recommended to restore factory settings and perform a basic configuration via router.miwifi.com before proceeding.

1. Download and extract [xmir-patcher](https://github.com/openwrt-xiaomi/xmir-patcher).
2. Download the latest stable OpenWRT firmware from [here](https://openwrt.org/toh/xiaomi/ax3200) and save it in the "firmware" folder of xmir-patcher.

Start the application and follow these steps in order (proceed only if each step is successful):

- Set IP address
- Connect to device (install exploit) → "SSH server are activated!" message will appear
- Install permanent SSH
- Install firmware (from "firmware" directory)

The router will automatically reboot with OpenWRT.

## Post-installation Fix for Softbrick After 6 Reboots (Blinking Orange LED)

After installation, run these commands via SSH to prevent softbrick caused by new bootloaders:

```sh
fw_setenv boot_fw1 "run boot_rd_img;bootm"
fw_setenv flag_try_sys1_failed 8
fw_setenv flag_try_sys2_failed 8
fw_setenv flag_boot_rootfs 0
fw_setenv flag_boot_success 1
fw_setenv flag_last_success 1
```

Reboot the router and check with `fw_printenv` that “flag_try_sys1_failed” is 8 or higher. If so, the fix was applied successfully.


## Unbrick

1. Start MIWIFIRepairTool.x86.
2. Select the stock firmware to flash in the first field, leave the rest unchanged.
3. Press the button at the bottom right.
4. Select "Ethernet".
5. Press the second button at the bottom right.
6. Connect the RJ45 cable to the WAN port of the router and to the PC. Hold down the reset button while reconnecting the power, and release the button when the orange LED starts blinking rapidly.
7. The tool will flash the firmware; at the end of the process, the power LED will blink blue rapidly.
8. Disconnect and reconnect the power to proceed with the initial configuration using the stock firmware.

**Note:**  
- It may be useful to set a static IP (192.168.31.100) on the ethernet interface.  
- In some cases, it may be useful to connect the cable to the first LAN port instead of the WAN port.

## Useful Links

- [info](https://github.com/mikeeq/xiaomi_ax3200_openwrt)
- [tutorial unbrick](https://www.youtube.com/watch?v=BoIQ4cNWR-Y)
- [xmir patcher fork (backup)](https://github.com/Razorbacktrack/xmir-patcher)