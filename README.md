# V7RC-ESP32-WIFI-LIB

這是一個專為 **ESP32** 開發的 **V7RC WiFi 控制函式庫**。  
能讓 Arduino/ESP32 專案透過 **WiFi (UDP 通訊)** 輕鬆與 **V7RC App** 通訊，適合用於遙控車、機器人、無人載具等專案。

---

## ✨ 功能特色
- WiFi AP 模式初始化（可自訂 SSID / 密碼 / 頻道）  
- 支援 UDP 通訊（Port 預設：6188）  
- 自動判斷連線狀態，無連線時回傳 `false`  
- 簡單 API 可讀取資料、解析控制訊號、檢查模式  
- 適合教學、比賽與開發  

---

## 📦 安裝方式
1. 下載此專案為 `.zip`  
2. 解壓縮後放入 Arduino 的 `libraries` 資料夾  
   ```
   文件/Arduino/libraries/V7RC_WIFI
   ```
3. 重新啟動 Arduino IDE  

---

## 🛠️ 使用範例

### 範例程式 (`V7RC_WIFI.ino`)
```cpp
#include <V7RC_WIFI.h>

V7RC_WIFI v7rc;

void setup() {
  Serial.begin(115200);
  // 建立 AP 熱點 (SSID, 密碼, 頻道)
  v7rc.setupWIFI("V7RC_WIFI", "12345678", 6);
}

void loop() {
  if (v7rc.connect()) {
    Serial.println(v7rc.readdata());

    if (v7rc.setMode("SRT")) {
      Serial.println("-------------------------------------------------------------------------");
      Serial.print("DATA 1：");
      Serial.println(v7rc.readSRTdata(1));

      Serial.print("DATA 2：");
      Serial.println(v7rc.readSRTdata(2));

      Serial.print("DATA 3：");
      Serial.println(v7rc.readSRTdata(3));

      Serial.print("DATA 4：");
      Serial.println(v7rc.readSRTdata(4));
    }
  }
}
```

---

## 📚 API 說明
| 函式 | 說明 |
|------|------|
| `setupWIFI(const char* ssid, const char* password, const int channel)` | 初始化 WiFi AP 模式 |
| `connect()` | 檢查是否有裝置連線並讀取 UDP 資料 |
| `readdata()` | 取得目前接收的字串 |
| `setMode(String mod)` | 判斷接收資料是否以特定字串開頭 |
| `readSRTdata(int sc)` | 讀取 SRT 模式中的數字資料 |

---

## 🔧 關鍵字高亮 (keywords.txt)
Arduino IDE 將自動高亮以下識別字：  

- **類別**：`V7RC_WIFI`  
- **函式**：`setupWIFI`, `connect()`, `readdata()`, `setMode(String mod)`, `readSRTdata(int sc)`  
- **常數**：函式庫內已定義  

---

## 📄 授權
MIT License – 可自由使用與修改。  
