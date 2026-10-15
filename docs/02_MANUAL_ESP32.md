# 🔌 Manual de Firmware & Hardware do ESP32

Este documento descreve como compilar, gravar e operar a placa física **ESP32 DevKit v1** para este projeto.

---

## 1. Hardware & Pinagem

O projeto foi projetado para funcionar utilizando **apenas a placa DevKit v1 e o cabo USB**, sem necessidade de protoboard ou componentes externos:

| Recurso | Pino (GPIO) | Função |
| :--- | :---: | :--- |
| **LED Onboard** | `GPIO 2` | Pulsação de inicialização e confirmação de visualização das histórias |
| **Botão BOOT** | `GPIO 0` | Botão físico na placa que dispara a chuva de corações no navegador da Gessy |
| **Comunicação** | `USB (COM)` | Terminal Serial (115200 baud) e gravação de firmware |

---

## 2. Particionamento de Memória (`partitions.csv`)

A tabela customizada expande a partição LittleFS para acomodar todos os assets estáticos no chip:

```csv
# Name,   Type, SubType, Offset,   Size
nvs,      data, nvs,     0x9000,   0x5000     (20 KB)
otadata,  data, ota,     0xe000,   0x2000     (8 KB)
app0,     app,  factory, 0x10000,  0x140000   (1.25 MB - Firmware C++)
spiffs,   data, spiffs,  0x150000, 0x2A0000   (2.625 MB - LittleFS Web)
coredump, data, coredump,0x3F0000, 0x10000    (64 KB)
```

---

## 3. Como Gravar na Placa com PlatformIO

1. **Configurar Credenciais Wi-Fi:**
   Copie `firmware_esp32/src/config.h.example` para `firmware_esp32/src/config.h` e preencha o SSID e senha da sua rede.

2. **Compilar e Gravar o Firmware:**
   ```bash
   pio run -t upload
   ```

3. **Gravar a Partição de Arquivos (LittleFS):**
   ```bash
   pio run -t uploadfs
   ```

4. **Monitorar o Terminal Serial:**
   ```bash
   pio device monitor -b 115200
   ```

