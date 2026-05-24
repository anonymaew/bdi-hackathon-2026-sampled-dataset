---
title: "ชุดข้อมูล EMR ผู้ป่วยความดันแบบติดตามยาว"
track: "Health"
domain:
  - "Clinical"
  - "Cardiovascular Research"
source:
  - "โรงพยาบาลศรีนครินทร์ มหาวิทยาลัยขอนแก่น"
total_records: 150000
sampled_records: 100
filetype:
  - "xlsx"

---

# ชุดข้อมูล EMR ผู้ป่วยความดันแบบติดตามยาว

## คำอธิบาย
ชุดข้อมูลผู้ป่วยโรคความดันโลหิตสูงจาก EMR จำนวนประมาณ **150,000 คน** (ตัวอย่าง **100 คน**) ข้อมูลบันทึกตลอดช่วงเวลา โดยแบ่งเป็น Periods (ช่วงละ 60 วัน) รอบวันที่วินิจฉัยโรค (baseline / `ht_onset`)

## ฟิลด์ข้อมูล

### ข้อมูลผู้ป่วย
| ฟิลด์ | คำอธิบาย |
|-------|----------|
| `age` | อายุผู้ป่วย ณ วันที่ baseline |
| `sex` | เพศ (`FEMALE` / `MALE`) |
| `identify_by` | วิธีการระบุเข้า dataset (`inferred_medication`, `icd10`, `medication`) |
| `ht_onset` | วันที่วินิจฉัยโรคความดันโลหิตสูง (baseline) |

### ค่าสัญญาณชีพ (Vitalsign): ตาม Period P
สัญญาณชีพ เช่น `resp`, `o2sat`, `temp`, `hr`, `ht`, `wt`, `bmi`, `sbp`, `dbp`

### ค่าห้องปฏิบัติการ (Lab): ตาม Period P
เช่น `fpg`, `hba1c`, `wbc`, `platelet`, `hemoglobin`, `lipid profile`, `thyroid`, `troponin`, `proBNP`, `electrolytes` ฯลฯ

### โรคประจำตัว (Comorbidity): ตาม Period P
เช่น `arrhythmias`, `atrial_fibrillation`, `cad`, `dementia`, `hf`, `stroke`, `dm`, `ckd`

### ยาที่ใช้ (Medication): ตาม Period P
เช่น `ARB`, `CCB`, `ACEI`, `beta_blocker`, `diuretics`, `hydralazine`, `neprilysin_inhibitor` ฯลฯ

### Period P
- **P = -1** : ก่อน ht_onset 30-90 วัน
- **P = 0** : ก่อนและหลัง ht_onset 30 วัน
- **P = 1** : 30-90 วันหลัง ht_onset
- ค่า P อื่นๆ เป็นช่วง 60 วัน

## โครงสร้างไฟล์
| ไฟล์ | รูปแบบ |
|------|--------|
| [`data_dictionary_hypertension_example.xlsx`](data_dictionary_hypertension_example.xlsx) | Excel (Data Dictionary) |

## โจทย์ / แนวทางวิเคราะห์
- **Risk Stratification**: ประเมินความเสี่ยงภาวะแทรกซ้อน (หัวใจ, ไต, สมอง)
- **Cohort Analysis**: วิเคราะห์ลักษณะผู้ป่วยกลุ่มต่างๆ
- **Treatment Effectiveness**: ประสิทธิภาพยาความดันแต่ละประเภท (ARB, CCB, ACEI ฯลฯ)
- **Predictive Model**: พยากรณ์ความดันโลหิต หรือความเสี่ยงหัวใจ/ไต
- **Comorbidity Analysis**: ความสัมพันธ์ระหว่างความดันกับโรคอื่น (เบาหวาน, CKD, หัวใจล้มเหลว)
- **Trend Analysis**: ติดตามแนวโน้ม SBP/DBP ตามเวลา

## หมายเหตุ
- ข้อมูลมีฟิลด์แบบ longitudinal (ตาม Period P)
