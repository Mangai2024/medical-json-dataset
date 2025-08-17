# 🏥 Patient Medical Data (JSON Format)

This repository contains **sample medical data** stored in a **nested JSON format**.  
It is designed for practice in:
- JSON parsing
- Data preprocessing
- Medical data analysis
- Converting JSON to CSV/DataFrame

---

## 📂 File Structure
- `patients.json` → Contains patient details (personal + medical information)

---

## 📑 Example Schema
Each patient record includes:
- **patient_id** → Unique ID
- **personal_info**
  - name, age, gender, contact (phone, email)
- **medical_info**
  - diseases (list)
  - medications (list of objects with name, dosage, frequency)
  - last_visit (date)

---

## 🚀 How to Use
### Python Example
```python
import json
import pandas as pd

# Load JSON
with open("patients.json", "r") as f:
    data = json.load(f)

# Normalize nested JSON to DataFrame
df = pd.json_normalize(data["patients"], 
                       record_path=["medical_info", "medications"],
                       meta=["patient_id", 
                             ["personal_info", "name"], 
                             ["personal_info", "age"], 
                             ["medical_info", "diseases"]])

print(df.head())
